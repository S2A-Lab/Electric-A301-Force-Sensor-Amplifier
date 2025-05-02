# Driver for the microcontroller and data transmission protocol

## Install driver for microcontroller

install the [STM32 Virtual COM Port Driver](https://www.st.com/en/development-tools/stsw-stm32102.html).

After you install the driver, COM device or serial port device will show when the amplifier board is plugged to your computer through the microUSB port.

## Communication protocol

The microcontroller encodes the analog reading and system time to a 11 byte package. The first 5 bytes are for analog reading data and last 5 bytes are for time. The last byte is a `0xFF` byte for frame check. 

|   TxFrame[0]   |   TxFrame[1]   |   TxFrame[2]   |   TxFrame[3]  |  TxFrame[4]  |  TxFrame[5]  |  TxFrame[6]  |  TxFrame[7]  |  TxFrame[8] | TxFrame[9] | TxFrame[10] |
|   ----------   |   ----------   |   ----------   |   ----------  |  ----------  |  ----------  |  ----------  |  ----------  |  ---------- | ---------- | ----------- |
|Analog (31 - 28)|Analog (27 - 21)|Analog (20 - 14)|Analog (13 - 7)|Analog (6 - 0)|Time (31 - 28)|Time (27 - 21)|Time (20 - 14)|Time (13 - 7)|Time (6 - 0)|     0xFF    |

Here is an example code to decode the data stream in Matlab: 

```Matlab
clear;clc;close all;
% === USER CONFIGURATION ===
comPort = "COM4";         % Change to your STM32 COM port
baudRate = 115200;        % Make sure it matches your USB CDC config
bufferSize = 11;          % One packet is 11 bytes

% === SETUP ===
s = serialport(comPort, baudRate);
% configureTerminator(s, "none");  % We're using custom delimiters
flush(s);  % Clear existing data

% === REAL-TIME PLOTTING ===
figure;
h = animatedline;
xlabel('Time (s)');
ylabel('ADC Value');
title('Live ADC Plot');
grid on;

startTime = datetime('now');
tic;
count = 0;
% === MAIN LOOP ===
while ishandle(h)
    if s.NumBytesAvailable >= bufferSize*100
        bytes = read(s, bufferSize*100, "uint8");
        % Decode 7-bit packed values
        [t, raw_data] = process_ADC7bit_data(bytes);
        
        % Add to plot
        addpoints(h, mean(double(t)/1000), mean(double(raw_data)));
        drawnow limitrate
        % count = count+length(raw_data);
    end
end

% === CLEANUP ===
clear s;

% === HELPER FUNCTION ===
function [t, v] = process_ADC7bit_data(raw_stream)
    % Find all potential frame endings
    frame_divide_idxes = [0; find(raw_stream == 255)'];
    frame_lengths = diff(frame_divide_idxes);
    
    % Only keep valid 11-byte frames
    valid_frame_idxes = frame_divide_idxes(frame_lengths == 11);
    if isempty(valid_frame_idxes)
        t = [];
        v = [];
        return;
    end

    % Index into raw_stream to extract all 11-byte frames
    data_indexes = repmat(valid_frame_idxes', 1, 11) + repelem(1:11,1,length(valid_frame_idxes));
    raw_data = reshape(raw_stream(data_indexes),[],11)';

    % raw_data(:,end)
    v4 = bitand(uint32(bitor(bitshift(raw_data(1,:),4), bitshift(raw_data(2,:),-3))),255);
    v3 = bitand(uint32(bitor(bitshift(raw_data(2,:),5), bitshift(raw_data(3,:),-2))),255);
    v2 = bitand(uint32(bitor(bitshift(raw_data(3,:),6), bitshift(raw_data(4,:),-1))),255);
    v1 = bitand(uint32(bitor(bitshift(raw_data(4,:),7), raw_data(5,:))),255);

    t4 = bitand(uint32(bitor(bitshift(raw_data(6,:),4), bitshift(raw_data(7,:),-3))),255);
    t3 = bitand(uint32(bitor(bitshift(raw_data(7,:),5), bitshift(raw_data(8,:),-2))),255);
    t2 = bitand(uint32(bitor(bitshift(raw_data(8,:),6), bitshift(raw_data(9,:),-1))),255);
    t1 = bitand(uint32(bitor(bitshift(raw_data(9,:),7), raw_data(10,:))),255);
    
    v = bitshift(v4,24)+bitshift(v3,16)+bitshift(v2,8)+v1;
    t = bitshift(t4,24)+bitshift(t3,16)+bitshift(t2,8)+t1;
    % t(t < 0) = t(t < 0) + 2^32;
end
```
