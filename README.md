# LDO Design with Power Supply Rejection Ratio:

# For Analog CMOS Project Electives:

![VL804_Analog_IC_Project_LDO-images-1](https://github.com/user-attachments/assets/f96dcb35-bd8f-46c8-8798-86c3c5a101e6)
![VL804_Analog_IC_Project_LDO-images-3](https://github.com/user-attachments/assets/6ab3c696-b1f5-46a7-9a7b-d5a52d19848f)
![VL804_Analog_IC_Project_LDO-images-4 (2)](https://github.com/user-attachments/assets/23201367-e941-48bc-9f9b-4b56e5773dd6)
![VL804_Analog_IC_Project_LDO-images-5](https://github.com/user-attachments/assets/8f1f7818-e0c4-4a18-a009-725c0db37e58)
![VL804_Analog_IC_Project_LDO-images-6](https://github.com/user-attachments/assets/77c7d568-13c7-4b0a-b807-d950621dfdf7)
![VL804_Analog_IC_Project_LDO-images-7](https://github.com/user-attachments/assets/6307c5d1-cffd-4a37-a1d6-6acb49c3b51b)
![VL804_Analog_IC_Project_LDO-images-8](https://github.com/user-attachments/assets/2a5c8395-b9ea-4845-84ae-cf9b3e470c4f)
![VL804_Analog_IC_Project_LDO-images-9](https://github.com/user-attachments/assets/b5e14317-4207-4a32-90b6-9d6aaee87107)
![VL804_Analog_IC_Project_LDO-images-10](https://github.com/user-attachments/assets/c5d0ea9e-d974-42d1-9842-d214e4581bbd)
![VL804_Analog_IC_Project_LDO-images-11](https://github.com/user-attachments/assets/6128746c-ca14-4eb9-b546-a092240413aa)
![VL804_Analog_IC_Project_LDO-images-12](https://github.com/user-attachments/assets/9d4443d2-b566-4bc1-8f8f-2796f627310d)
![VL804_Analog_IC_Project_LDO-images-13](https://github.com/user-attachments/assets/32923f59-7fbc-4cb6-bbbe-a7d41c785daa)
![VL804_Analog_IC_Project_LDO-images-14](https://github.com/user-attachments/assets/adf82ade-4399-4bf9-8e2c-8aa3651e1c38)
![VL804_Analog_IC_Project_LDO-images-15](https://github.com/user-attachments/assets/5f4e1cb4-5fc0-4821-8851-79548cadaa16)
![VL804_Analog_IC_Project_LDO-images-16](https://github.com/user-attachments/assets/287033f2-5fcb-469e-801f-ff8eac6db5ce)
![VL804_Analog_IC_Project_LDO-images-17](https://github.com/user-attachments/assets/dd4ff310-cf57-4c3e-aed8-088e9f316d27)
![VL804_Analog_IC_Project_LDO-images-19](https://github.com/user-attachments/assets/487090bc-7bea-4d8f-8c65-fb22b98bf256)
![VL804_Analog_IC_Project_LDO-images-18](https://github.com/user-attachments/assets/8347dc29-5d6a-4e64-adc6-e2ce663b7e13)

## Observations: 

* The phase margin under light load is 70°, which is higher than under heavy load conditions.
* In externally compensated LDOs, the second pole remains constant, but the first pole and unity-gain bandwidth increase with load current leading to better phase margin at light load since the second pole is further from the unity-gain bandwidth.
* In internally compensated LDOs, the unity-gain bandwidth remains constant, while both poles shift with increasing load. At light load, the second pole moves closer to the unity-gain bandwidth, resulting in higher phase margin.
* Therefore, light load conditions generally result in greater phase margin and system stability compared to heavy load conditions.

## Key Takeaways:

* Circuit was unstable without miller compensation with peaky loop gain at 1st pole.
* By parametric sweep and theoretical calculator stability was improved simultaneously.
* Make stability dependency on Miller capacitance Cc and got PSRR at Phase Margin of 45 and 70 degree respectively.
* DC close loop PSRR at phase margin of 45 degree was coming out -58 dB at 1Hz at 10mA
* DC close loop PSRR at phase margin of 70 degree was coming out -71 dB at 1Hz at 50mA

# Schematic to Layout GDS for LDO Project with Internship:

# Normal Miller capacitor LDO:

## Sizing by gm/Id methodology:

<img width="525" height="340" alt="image" src="https://github.com/user-attachments/assets/6684d547-61a7-402a-9e35-299937cc5e21" />

## Square Law vs gm/Id Methodology:

| Square Law-based Approach | Techplot-based Approach |
|---------------------------|--------------------------|
| As the length of the technology node decreases, the standard equation of `gm/Id = 2/Vov` is not valid and instead it follows a linear relation. **Thus, we can’t apply square law for lower nm technology nodes.** | While making **techplots**, we ask the tool to calculate the individual values of `gm/Id`, `gm·ro`, `ft`, and `Id/W` at different values of length instead of depending on the equation, and thus we get the exact curve which incorporates the short channel effects. |
| Design will **take more time** for lower technology nodes as second-order effects come in picture. | Design will comparatively **take less time** as we can have a script to design the entire topology. |
| More accurate as **exact values are considered**. | **Can be less accurate** if the dataset taken to plot **techplots** is of less resolution. |

### Why gm/Id over square Law:

* I am using the gm/Id method to size the transistors as I was working with relaxed constraints and the speed to design the circuits is comparitively faster for gm/Id methodology.
* Most importantly as I am working with 45nm technology node short channel effects can come in the picture which will be taken care by the gm/Id methodology.

<img width="556" height="350" alt="image" src="https://github.com/user-attachments/assets/46c11bb5-1e12-4bae-bfda-bbf08efd2f85" />

<img width="799" height="560" alt="image" src="https://github.com/user-attachments/assets/e519dafe-0be0-41bd-90e3-eb7d42aea9ca" />

### Techplots for gm/Id Methodology:
* Comparison of different FOMs at different lengths:
<img width="473" height="124" alt="image" src="https://github.com/user-attachments/assets/2dcdf646-1f66-4bea-9da4-304b9ebde9f4" />

* We chose the Vds to be 0.4 mV, and we expect that to result in some error because the Vds across every MOSFET might not be the same after sizing the circuit under a particular load. It is very possible that the Vds across the MOSFETs can change under different values of load current. The above phenomenon can be understood from the output log files mentioned below.

### NMOS Techplots after Python postprocessing - Id/W:
<img width="1536" height="754" alt="image" src="https://github.com/user-attachments/assets/88b6cc59-109b-4c45-91df-e867949cbd3e" />

### NMOS Techplots after Python postprocessing - gmro:
<img width="1536" height="754" alt="image" src="https://github.com/user-attachments/assets/43d6f388-be30-4d0c-8245-720d3d90389f" />

### NMOS Techplots after Python postprocessing - fT:
<img width="1536" height="754" alt="image" src="https://github.com/user-attachments/assets/2a7b10fc-6e42-45fc-a825-e7f4018fcb00" />

### PMOS Techplots after Python postprocessing - Id/W:
<img width="1536" height="754" alt="image" src="https://github.com/user-attachments/assets/f0ece32c-ca81-47b5-8058-f1a45b8670ff" />

### PMOS Techplots after Python postprocessing - gmro:
<img width="1536" height="754" alt="image" src="https://github.com/user-attachments/assets/090339f0-abbf-45fa-b7f5-d343302f1f6d" />

### PMOS Techplots after Python postprocessing - fT:
<img width="1536" height="754" alt="image" src="https://github.com/user-attachments/assets/449a26ec-6de4-45e5-a618-fac431199786" />

### Observations on Technology Scaling Effects:
<img width="855" height="299" alt="image" src="https://github.com/user-attachments/assets/7b4e980e-0b4b-4028-991d-1e845c6d368e" />

## gm/Id Methodology and Flow for Transistor Sizing:

<img width="738" height="475" alt="image" src="https://github.com/user-attachments/assets/f488dbb9-c3b5-4c41-8793-8475c5d7cede" />

<img width="700" height="495" alt="image" src="https://github.com/user-attachments/assets/e6538cbc-7f4f-4dee-8578-deac8f2e2daf" />

<img width="705" height="509" alt="image" src="https://github.com/user-attachments/assets/9e2f8b7d-721f-4f8f-86af-32c6b87118ef" />

<img width="711" height="423" alt="image" src="https://github.com/user-attachments/assets/60c8a1e9-e306-49af-9ccc-8acba25f2f5b" />

<img width="715" height="491" alt="image" src="https://github.com/user-attachments/assets/ac2b7c80-528d-4cc9-9153-88d1cc151033" />

## Sizing of transistors for 45nm Technology Node by gm/Id methodology:

<img width="1544" height="1940" alt="image" src="https://github.com/user-attachments/assets/dd4f310e-5253-4f63-8c22-125e6496fcd4" />

<img width="1074" height="1650" alt="image" src="https://github.com/user-attachments/assets/8affb640-f2da-406f-9707-46c7779d585b" />

## DC Operating Point:

![Op Screenshot from 2025-05-15 14-38-56](https://github.com/user-attachments/assets/b2362b37-6e7d-4fa6-9ae5-f7e8dabc0139)

![Op Screenshot from 2025-05-15 14-39-07](https://github.com/user-attachments/assets/c7a19a26-2e8b-4373-965f-b74dc9169380)

## Loop Gain - Stability,Phase Margin:

![Screenshot from 2025-06-12 13-39-56](https://github.com/user-attachments/assets/f5cdd592-0771-44b4-a44d-1f6733def59e)

![Loop Gain Screenshot from 2025-05-15 02-47-50](https://github.com/user-attachments/assets/618ed5ce-bbd8-4e65-861b-46f96fef3da2)

### Explanation of the artifact used for Loop Gain:-

* In order to calculate the loop gain we have given a RC circuit in the feedback loop along with a AC source with amplitude 1 (as we want to maintain an AC voltage of 1V) at the output.
* At the same time we also need to bias the circuit and provide a dc voltage to the gate of the nmos in the differential amplifier and for this we are giving the RC circuit which will prevent the flow of dc current to ground but will send any AC signal at the output to ground at high frequency.
* Also the drop across the resistor will be very less as we have given a very high resistance with very negligible current (since current going into the gate of the mosfet is zero). Thus we will bias the circuit and also calculate the loop gain.

## Open Loop PSRR:

![Screenshot from 2025-06-12 13-41-28](https://github.com/user-attachments/assets/74eed35e-6a09-4ad5-a177-a464b16a8a8e)

![OLPSRR Screenshot from 2025-05-15 04-43-32](https://github.com/user-attachments/assets/e18ec355-2b21-40d8-a431-ff6494aa7f9d)

### Explanation of the artifact used for Open Loop PSRR:-

* In order to calculate the open loop PSRR we need to send an AC signal from the source which in our case is VDD. Here we are giving an AC=1 signal in the source. This signal is given to the source of the passfet and the source of pmos in the diffamp.
* We will ideally want very bad PSRR in the diffamp as we want the OTA output to have all the AC noise such that Vsg of pmos = 0 (small signal analysis).Thus all the noise will get rejected and we will get a noise free dc voltage at the output of the LDO.
* Here in order to calculate the open loop PSRR we have a RC circuit to bias the differential amplifier. You can see AC=0 in the circuit indicating that there is an open loop in the circuit. From here we have calculated the open loop PSRR in the circuit.
* Since, there is no feedback in the circuit we can thus say that there will be noise at the output and thus the rejection will be very poor.

#### Note:
* Always observe the Vota output in volts because it will give you the insight into what AC voltage is coming into the gate of the passfet. It should be close to VDD.
* The closer it is to 1v the better it is for a very bad PSRR at the output as the Vsg value will be close to 0.
  
## Close Loop PSRR:

![Screenshot from 2025-06-12 13-41-08](https://github.com/user-attachments/assets/d0bc97e7-e499-436e-a1e5-d8bea25f7ddf)

![CLPSRR Screenshot from 2025-05-15 04-41-59](https://github.com/user-attachments/assets/d5db32cb-40b6-40cd-b10d-d0adb4e54e56)

### Explanation of the artifact used for Close Loop PSRR:-
* In this case we can see that we have given a AC source in the voltage source VDD. We want to see the negative feedback in the circuit due to which we will get the output voltage cancelled out (small signal analysis).
* Here we should observe a high PSRR according to our specifications ( 60db) which tells us that our sizing is perfect. For this circuit we have given a feedback from the output terminal to the input of the diffamp which indicates the feedback path.

## Layout:
## Layout Schematics:

![Layout_Schematic](https://github.com/user-attachments/assets/c3046cf2-3d3b-44c1-ab11-4005329054e2)

## Layout of Normal LDO:

![Layout 1](https://github.com/user-attachments/assets/d69964c8-b10e-4c01-b954-f7fb052c7dd9)

![Layout 2](https://github.com/user-attachments/assets/649c3e36-579a-4d05-b3df-2d24424d42b7)

## Verification DRC,LVS,ERC checks:

![Screenshot from 2025-06-12 19-24-22](https://github.com/user-attachments/assets/282ff587-b917-4685-b99d-7efebd4ae8c3)

![Screenshot from 2025-06-12 19-25-50](https://github.com/user-attachments/assets/8630272a-8f56-40a0-9a84-26d4d87d536c)

## Parasitic Extraction:

![Screenshot from 2025-06-12 20-46-45](https://github.com/user-attachments/assets/9d9be5a0-57df-4468-a96f-0764a3ddf7ab)

![Screenshot from 2025-06-12 20-47-19](https://github.com/user-attachments/assets/07924194-a10c-4309-976a-2c9c3eaa53c8)

![Screenshot from 2025-06-12 20-38-55](https://github.com/user-attachments/assets/ff8caa0f-f0ba-40b9-8e29-e5584d433ce0)

![Screenshot from 2025-06-12 20-38-07](https://github.com/user-attachments/assets/aa0e00b7-077d-4d61-be6d-a81737a6ae77)

# LDO with passfet multiplier 4:

## Stability:

![Screenshot from 2025-06-12 15-37-25](https://github.com/user-attachments/assets/abe43361-5624-4f12-b2f0-bea48b55d505)

![Screenshot from 2025-06-12 16-05-47](https://github.com/user-attachments/assets/cdcfd71b-bfce-4568-9e78-158850ee9a86)

## DC operating Point:

![Screenshot from 2025-06-12 15-36-13](https://github.com/user-attachments/assets/d4ed3f43-a130-4318-b82f-e91738934e1c)

## Open Loop PSRR: 

![Screenshot from 2025-06-12 16-09-09](https://github.com/user-attachments/assets/38491393-a4ea-45de-a91c-b9c6ee77c7a1)

![Screenshot from 2025-06-12 16-30-10](https://github.com/user-attachments/assets/2e1203f5-7461-44cc-9aa4-65c2da4ff83c)

## Close Loop PSRR:

![Screenshot from 2025-06-12 16-39-06](https://github.com/user-attachments/assets/0b129cea-0354-4d57-bf8b-70edcdf630d0)

![Screenshot from 2025-06-12 16-44-17](https://github.com/user-attachments/assets/0bbe6f65-3778-43ff-b1d3-7467bc0ac261)

![Screenshot from 2025-06-12 17-49-55](https://github.com/user-attachments/assets/195a296f-45ff-4c51-9b07-738f755cb2b5)

![Screenshot from 2025-06-12 18-55-57](https://github.com/user-attachments/assets/86671f75-252c-4d21-93a1-b404a5c35e3f)


## Layout: 

![Screenshot from 2025-06-12 18-50-39](https://github.com/user-attachments/assets/0ecff5cf-8355-402f-b614-bfea897c9630)

![1 1](https://github.com/user-attachments/assets/a42ab2b6-9cb0-4ed9-b157-3ff3b5705995)

![1 2](https://github.com/user-attachments/assets/721d2746-9b50-4f2c-9d20-0bc6ef6fadbf)

# LDO with multiplier miller cap 5n & parametric:

![Screenshot from 2025-06-12 21-57-47](https://github.com/user-attachments/assets/f6927b75-8fc2-421e-aff2-c291251d9d78)

## Stability:

![Screenshot from 2025-06-12 22-06-27](https://github.com/user-attachments/assets/1976b6d6-12b3-49e9-abf4-cfdcc1ca963b)

## Closed Loop PSRR: 

![Screenshot from 2025-06-12 22-45-14](https://github.com/user-attachments/assets/47140aa0-3b3f-400f-946c-6a62a1ee8964)

![Screenshot from 2025-06-12 22-42-13](https://github.com/user-attachments/assets/5c999688-3d97-479a-898c-7e9ffab66b9c)

![Screenshot from 2025-06-12 22-44-56](https://github.com/user-attachments/assets/4d88b858-c5d3-4557-923a-0512485b70db)

![Screenshot from 2025-06-12 21-57-31](https://github.com/user-attachments/assets/0da6adfd-967d-4522-8f13-bd301bff5211)

# Key Takeaways:

* Stability of Normal LDO with Phase Margin of 78.71 degree at 8.15kHz.
* CLPSRR of -44.4dB at 1 Hz for miller compensated of 5nF normal LDO.
* Prepared optimised layout with area single LDO is 1312.13 um^2 with clean DRC,LVS,ERC, and Parasitic Extraction.
* Stability of LDO with Multiplier of 4x with miller compensated - Phase Margin of 69.72 degree at 25.8kHz.
* CLPSRR of -85.31dB at 1 Hz for miller compensated of 5nF multiplier LDO.
* Prepared optimised Layout with Area multiplier LDO is 3039.39 um^2 with clean DRC Checks.
