# Autonomous-Vehicle
A vehicle designed from scratch (from very scratch) and driven autonomously using a MLP.

---

## Methods/Hardware used

1. Multilayer Perceptron
2. Sockets for live streaming
3. Microcontroller (Atmega328p as arduino for transmitter and receiver)
4. RF communication (nRf24L01+ for wirelessly controlling the bot)
5. CPU on the bot(Raspberry pi 3 and camera for video capturing)

---
## Block Diagram and overall flow of Project

<img src="images/block.png" height="400" alt="Screenshot"/>

# Description
1. Flash Arduino : Flash `rc_keyboard_control.ino` to Arduino and run `rc_control_test.py` to drive the rc car with keyboard. (testing purpose)
2. Pi Camera calibration: Take multiple chess board images using pi camera at various angles and put them into `chess_board` folder,  
       run `picam_calibration.py` and it returns the camera matrix, those parameters will be used in `rc_driver.py`
3. Collect training data and testing data: First run `collect_training_data.py` and then run `stream_client.py` on raspberry pi. User presses keyboard to drive
       the RC car, frames are saved only when there is a key press action. When finished driving, press `q` to exit, data is saved as a npz file.
4. Neural network training: Run `mlp_training.py`, depend on the parameters chosen, it will take some time to train. After training, model will be saved in   
      `mlp_xml` folder
5. Cascade classifiers training : trained stop sign and traffic light classifiers are included in the `cascade_xml` folder, 
6. Self-driving in action: First run `rc_driver.py` to start the server on the computer and then run `stream_client.py` and `ultrasonic_client.py` on raspberry        pi.
