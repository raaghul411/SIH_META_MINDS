% MATLAB Code for Rail Defect Detection - Crack and Object Detection

% Parameters
Fs = 44100; % Sampling frequency for acoustic sensor
t = 0:1/Fs:2; % Time vector for 2 seconds of data
frequency = 5000; % Frequency of the acoustic wave in Hz

% Simulate sensor data (ultrasonic, acoustic)
acoustic_signal_no_crack = sin(2*pi*frequency*t); % Acoustic signal without crack
ultrasonic_signal_no_crack = chirp(t, 1000, 2, 5000); % Ultrasonic signal without crack

% Crack Detection Logic
crack_detected = true; % Assume crack is detected
acoustic_signal_with_crack = acoustic_signal_no_crack * 1.5 + 0.2 * rand(1, length(t)); % Acoustic signal with crack
ultrasonic_signal_with_crack = ultrasonic_signal_no_crack * 1.3 + 0.1 * rand(1, length(t)); % Ultrasonic signal with crack

% Object Detection using Microwave Sensor
object_distance = randi([0, 300]); % Random object distance in meters (train's path)
safe_stopping_distance = 200; % Safe stopping distance for the train
object_detected = object_distance < safe_stopping_distance; % Detect if object is too close

% Optimized plot ranges for sensor signals
x_min = 0;  % Min time (seconds)
x_max = 0.1;  % Max time (zoomed in on first 0.1 seconds)
y_min_acoustic = -2;  % Min amplitude for acoustic signal
y_max_acoustic = 2;   % Max amplitude for acoustic signal
y_min_ultrasonic = -2; % Min amplitude for ultrasonic signal
y_max_ultrasonic = 2;  % Max amplitude for ultrasonic signal

% Display signals for acoustic sensor without crack
figure;
subplot(2,1,1);
plot(t, acoustic_signal_no_crack, 'b');
xlabel('Time (s)');
ylabel('Amplitude');
xlim([x_min, x_max]);  % Zoom in on the first 0.1 seconds
ylim([y_min_acoustic, y_max_acoustic]);  % Set Y-axis range
title('Acoustic Signal Without Crack');

% Display signals for acoustic sensor with crack
subplot(2,1,2);
plot(t, acoustic_signal_with_crack, 'r');
xlabel('Time (s)');
ylabel('Amplitude');
xlim([x_min, x_max]);  % Zoom in on the first 0.1 seconds
ylim([y_min_acoustic, y_max_acoustic]);  % Set Y-axis range
title('Acoustic Signal With Crack');

% Display signals for ultrasonic sensor without crack
figure;
subplot(2,1,1);
plot(t, ultrasonic_signal_no_crack, 'b');
xlabel('Time (s)');
ylabel('Amplitude');
xlim([x_min, x_max]);  % Zoom in on the first 0.1 seconds
ylim([y_min_ultrasonic, y_max_ultrasonic]);  % Set Y-axis range
title('Ultrasonic Signal Without Crack');

% Display signals for ultrasonic sensor with crack
subplot(2,1,2);
plot(t, ultrasonic_signal_with_crack, 'r');
xlabel('Time (s)');
ylabel('Amplitude');
xlim([x_min, x_max]);  % Zoom in on the first 0.1 seconds
ylim([y_min_ultrasonic, y_max_ultrasonic]);  % Set Y-axis range
title('Ultrasonic Signal With Crack');

% Object detection output
if object_detected
    disp(['Object Detected at ' num2str(object_distance) ' meters! Emergency braking required.']);
else
    disp('No objects detected in the path of the train.');
end

% Predictive analysis (time series forecast for track maintenance and crack progression)
future_points = 100; % Predict for next 100 time steps (representing years)
past_acoustic = acoustic_signal_with_crack(end-future_points+1:end); % Past data with crack
predicted_acoustic = predict_future_signal(past_acoustic, future_points);

% Prediction: Time until track maintenance is needed and when crack becomes a threat
maintenance_threshold = 1.8; % Threshold amplitude for triggering track maintenance
threat_threshold = 2.5; % Threshold amplitude when crack becomes a major threat

% Convert time steps into years for more intuitive output
total_years = 10; % Predict for a total of 10 years
time_step_years = total_years / future_points; % Time step in years

% Determine when to change the track (cost-efficient) and when crack becomes a threat
maintenance_time = find(predicted_acoustic >= maintenance_threshold, 1);
threat_time = find(predicted_acoustic >= threat_threshold, 1);

maintenance_years = maintenance_time * time_step_years;
threat_years = threat_time * time_step_years;

% Display future acoustic signal and prediction with years and damage
figure;
plot((1:future_points) * time_step_years, predicted_acoustic); % X-axis in years
title('Predicted Acoustic Signal with Crack Progression');
xlabel('Years');
ylabel('Damage');
xlim([0, total_years]);
ylim([0, 3]);
hold on;

% Highlighting maintenance and threat times on the graph
if ~isempty(maintenance_time)
    plot(maintenance_years, predicted_acoustic(maintenance_time), 'go', 'MarkerSize', 10);
    disp(['Track maintenance should be scheduled after ' num2str(maintenance_years, '%.2f') ' years.']);
else
    disp('No track maintenance needed in the predicted range.');
end

if ~isempty(threat_time)
    plot(threat_years, predicted_acoustic(threat_time), 'ro', 'MarkerSize', 10);
    disp(['Crack will become a major threat after ' num2str(threat_years, '%.2f') ' years.']);
else
    disp('Crack will not become a major threat in the predicted range.');
end

legend('Predicted Acoustic Signal', 'Maintenance Required', 'Major Threat');
hold off;

% Function for simple signal prediction using linear extrapolation
function predicted_signal = predict_future_signal(past_data, future_steps)
    trend = mean(diff(past_data)); % Simple linear trend calculation
    predicted_signal = past_data(end) + (1:future_steps) * trend;
end

