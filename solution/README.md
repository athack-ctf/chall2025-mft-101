# How to Solve the Challenge?

MFT stands for "Master File Table," which is a crucial file that stores information about every file and directory on a volume, including their location, size, creation date, and other metadata, essentially acting as a database to track all files on the drive; every file on an NTFS partition has at least one corresponding entry in the MFT. 

We have few questions to answer about the secret file. First, we need a tool that help us parse the MFT file to get as much info from it, there are several tools that can do the job but our go tool is `MFTECmd` (cli tool) by Eric Zimmerman (Zimmerman has a wide variation of tools to help DFIR people doing the job). We can find the list of the tools [here](https://ericzimmerman.github.io/#!index.md).

`Note: I am using windows here as windows forensics tools that are compatible  with windows OS are numerous and powerful, unlikely in linux and vice versa`

Command: 
`MFTECmd.exe -f 'path/to/mft/file' --csv 'path/to/output/result'`
here we used the output result to be  in csv format so we can deal with it easily later, but Zimmerman tools support json also.

![image](https://github.com/user-attachments/assets/3712c7fe-29e7-4310-9b41-81289624e517)

Having the parsed data in hand, we can open it using MS Excel as it is a csv file, but for our purpose we will use another tool by Eric zimmerman called `Timeline Explorer` (gui) which was made for the purpose. You can find the tool in the same link above. 
Opening our csv file we got from `MFTECmd` in timeline Explorer will look like: 

![image](https://github.com/user-attachments/assets/0cc970bf-525c-428f-bc7e-8e08c68a6773)

Since in the description they specified that a secret file was left in the Desktop we can filter by path in Timeline Explorer:

![image](https://github.com/user-attachments/assets/08d5bbb2-6414-4bbf-9729-201b718558d4)

Notice `secret.txt` file under the folder `important` on the Desktop. We got our file, let's answer the questions and form the flag:
- What is the MFT entry number of the secret file ?
  ![image](https://github.com/user-attachments/assets/6812eabf-855f-4d77-a97a-5bc93db5db7e)

- What is the size of the secret file in bytes ?
![image](https://github.com/user-attachments/assets/63297d55-35df-4c22-94ce-df500df680c7)

- What is the creation time of the secret file in UTC ? (format: YYYY-MM-DD HH:MM:SS)
![image](https://github.com/user-attachments/assets/50f2ede8-0baf-4c98-bdee-3d8d837a5a00)
Know that Zimmerman tools show time in UTC by default.

The final flag would be:
`ATHACKCTF{580_87_2025-01-25 06:41:21}`
