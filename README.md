# DaCapo:An On-Device Learning Scheme for Memory-Constrained Embedded Systems

DaCapo is a backpropagation scheme that enables on-device learning in memory-constrained embedded systems. DaCapo stores only the output of certain layers, known as checkpoints, and discards the others. The discarded outputs are recomputed during backpropagation from the nearest checkpoint in front of them. In order to minimize the recomputation occurrences, DaCapo optimally plans the checkpoints to be stored in the SRAM memory at a particular phase of the backpropagation, and thus replaces the checkpoints stored in memory as the backpropagation progresses. 

### Requirements

-   STM32CubeIDE v1.12.0
-	NUCLEO-F429ZI board
-   YOKOGAWA WT330 power meter (Any power meter is fine as long as it can be connected to a PC. We provide a script for this power meter.)
-   Python v3.9.6

---


### File Structure

```
📦Artifact
 ┣ 📂AIfESFiles
 ┃ ┣ 📂Models
 ┃ ┃ ┣ 📂DepthEstimation
 ┃ ┃ ┃ ┣ 📂Core
 ┃ ┃ ┃ ┃ ┣ 📂Inc
 ┃ ┃ ┃ ┃ ┣ 📂Src
 ┃ ┃ ┣ 📂FOMO
 ┃ ┃ ┣ 📂TinyVGG
 ┃ ┣ 📂STM32CubeIDEProject
 ┃ ┃ ┗ 📜AIfES_FLASH.zip
 ┣ 📂DaCapoFiles
 ┃ ┣ 📂Models
 ┃ ┃ ┣ 📂DS-CNN
 ┃ ┃ ┃ ┣ 📂Core
 ┃ ┃ ┃ ┃ ┣ 📂Inc
 ┃ ┃ ┃ ┃ ┣ 📂Src
 ┃ ┃ ┃ ┗ 📂NN
 ┃ ┃ ┃ ┃ ┗ 📂Inc
 ┃ ┃ ┣ 📂DepthEstimation
 ┃ ┃ ┣ 📂FOMO
 ┃ ┃ ┣ 📂MobileNet
 ┃ ┃ ┣ 📂TinyVGG
 ┃ ┣ 📂STM32CubeIDEProject
 ┃ ┃ ┗ 📜DaCapo.zip
 ┗ 📜power_calculation_script.py
```

To use our project, navigate to the **📦Artifact** directory. 
Here, you will find two subdirectories: one for **📂AIfESFiles** and another for **📂DaCapoFiles**. 
Additionally, there is a power measurement script written in Python `(power_calculation_script.py)`. 
Each of these directories contains two more subdirectories. 
The **📂Models** directory holds files for different models, and the **📂STM32CubeIDEProject** directory contains an archived version of the STM32 Project.

---

### Configuration (AIfES+Flash)

1.	Launch the STM32CubeIDE application and import the archived version of the STM32 project into your current workspace. The project archive file is located at `Artifact/AIfESFiles/STM32CubeIDEProject/AIfES_FLASH.zip`. It is important not to modify any settings during the import process.
2.	Navigate to `Artifact/AIfESFiles/Models` and select the directory of the model you wish to execute.
3.	After selecting a directory, copy all files in `Artifact/AIfESFiles/Models/SelectedModel/Core/Inc`, and overwrite them into `Core/Inc` of the project you imported in step 1.
4.	Copy `my_model.c` in `Artifact/AIfESFiles/Models/SelectedModel/Core/Src` and overwrite it into `Core/Src` of the project you imported in step 1.
5.	Ensure that the board is connected and click on the debug button (or Run) to start the execution.
> To check the result output screen, a method of connecting the serial communication port is available.

---

### Configuration (DaCapo)

1.	Launch the STM32CubeIDE application and import the archived version of the STM32 project into your current workspace. The project archive file is located at `Artifact/DaCapoFiles/STM32CubeIDEProject/DaCapo.zip`. Remember not to change any settings while importing.
2.	Navigate to `Artifact/DaCapoFiles/Models` and select the directory of the model you wish to execute.
3.	After selecting a directory, copy a file `input_image.h` in `Artifact/DaCapoFiles/Models/SelectedModel/Core/Inc`, and paste them into `Core/Inc` of the project you imported in step 1.
4.	Copy a file `main.c`in `Artifact/DaCapoFiles/Models/SelectedModel/Core/Src`, and paste them into `Core/Src` of the project you imported in step 1.
4.	Copy all files in `Artifact/DaCapoFiles/Models/SelectedModel/NN/Inc` and paste it into `NN/Inc` of the project you imported in step 1.
5.	Ensure that the board is connected and click on the debug button (or Run) to start the execution.

---

### Power Measurement

1.	Connect the NUCLEO-F429ZI to a power meter to measure power consumption. To do this, remove the jumper from JP5 and connect the power meter to measure current consumption.
2.	In our code, the function `send_byte` is used to send a signal to the PC to stop gathering data from the power meter.
3.	For proper synchronization between the power meter and the board, execute the power meter script before executing the project.
> Here, too, the correct serial communication porting process is required.
