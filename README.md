# slip-cont-traj-adapt


This repository includes the codes and sample dataset to run the experiments for the proposed slip avoidance controllers by trajectory adaptation.


**Model Training**
=====
A sample data set of the moving task is included in /data_set directory. The frank robot executes a linear motion in XY plane in the base frame. The robot is controlled by libfranka's Cartesian Velocity controller. As such, a trapezoidal profile for velocity for X direction is built (the velocity in Y drectoin comes from scaling the X velocity) for executing the task. A box shaped object is used as the training object and two uSkin tactile sensors from XELA ROBOTICS are attached to the 3d printed fingers mounted on franka gripper. A wrist camera reads the pose of an Aruco marker attached on the objects to detect objec's relative motion w.r.t the EE and generating the binary slip ground truth values. The data set include synchronized tactile (2 x $D \in R^{48}$), robot ($q \in R^7$, $dq \in R^7$, $EE_{pose} \in R^{16}$, and $EE_{vel} \in R^6$), and marker pose data ($P \in R^7$). 

        run gen_dataset.py to create data sequences for training.

Edit the data set and output folder directories in the script. We use two slip classification models. One is a slip detection model which uses a history of tactile data to predicit the slip binary state at current time step. The second model is an action-conditioned modek which use tatctile hisory alongside future robot trajectory for slip prediction. The training scripts for these models are in /slip_detection and \AC_slip_prediction directories respectively. 
