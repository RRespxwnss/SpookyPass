# SpookyPass

# Description
SpookyPass is a reverse engineering lab that involves analyzing a compiled binary in order to understand its internal logic and uncover the implemented authentication mechanism. When starting the challenge, the program presents a simple “spooky”-themed interface and prompts the user to enter a password, returning an error message if the provided value is incorrect.

# Initial Reconnaissance
To begin the analysis, two initial reconnaissance steps were performed. The first used the Certutil utility to inspect the binary and gather relevant information about its structure and any embedded data. Next, the Strings tool was applied to extract readable text from the executable, allowing the identification of sensitive information, validation patterns, or clues about the application's internal logic.

These initial analyses were essential for guiding the next steps of the reverse engineering process more precisely. Through the use of Certutil, it was possible to identify the complete password used in the authentication process. However, there was no direct access to execute the binary and validate the input, which required a deeper level of analysis.

Therefore, it became necessary to proceed with a more detailed static analysis of the binary, aiming to fully understand the validation logic implemented and confirm the internal behavior of the application.

<p align="center">
  <img src="https://github.com/user-attachments/assets/eee98407-b43e-415e-914a-65b1cdd67365" width="32%"/>
  <img src="https://github.com/user-attachments/assets/40c0f36d-1a65-4f73-b8f2-c4f4c36a9c42" width="32%"/>
  <img src="https://github.com/user-attachments/assets/8a38aad9-e7f5-4123-b152-7a6aa5bf40dc" width="32%"/>
</p>

# Ghidra Analysis
After the initial reconnaissance steps, the analysis progressed using Ghidra, enabling a deeper inspection of the binary. While navigating through the decompiled code, it was possible to identify the main function responsible for the program’s execution flow, including user input handling and the password validation process.

The verification is performed using the strcmp function, where the user-provided input is directly compared to a fixed string embedded in the binary. The absence of any protection mechanism indicates that the password is stored in plain text and can be easily identified through static analysis.

However, a deeper inspection of the execution flow revealed that the flag is not stored as a plain string. Instead, it is dynamically constructed within a for loop. This loop iterates over a data structure in memory, performing sequential operations—such as assignments or transformations—to build the flag character by character.

By carefully analyzing this section, it was possible to understand how the values are manipulated within the loop and manually reconstruct the final flag without executing the binary. Understanding how the for loop operates, including its boundaries, iteration index, and data sources, was essential to fully recover the information.

Further analysis showed that the variable parts plays a key role in building the flag. The values stored in parts are not directly readable characters but numerical values corresponding to the ASCII table.

Based on this logic, the program uses these values inside the loop to dynamically assemble the flag by converting each number into its respective character. By mapping the values stored in parts to their ASCII equivalents, it was possible to fully reconstruct the flag manually, without executing the binary.

This understanding was crucial to completing the challenge, demonstrating how the flag was obfuscated in a simple yet effective way that required deeper analysis of the program’s execution flow.

See the images below.

<p align="center">
  <img src="https://github.com/user-attachments/assets/6cabefa3-b0e7-4db3-b7b2-a288956c7259" width="32%"/>
  <img src="https://github.com/user-attachments/assets/c48ec8a6-c920-4836-ac74-d2fcc6d8db1a" width="32%"/>
  <img src="https://github.com/user-attachments/assets/d6926908-f394-4a2b-a955-d9cbf767cab8" width="32%"/>
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/e15d48c7-3c64-4b7f-b9c4-4fd4c15db42a" width="32%"/>
  <img src="https://github.com/user-attachments/assets/a3dc2ff7-0f64-4fe2-8b65-d442d356873f" width="32%"/>
  <img src="https://github.com/user-attachments/assets/bf57e347-4fb3-4df0-b4c1-d9170fce5dd8" width="32%"/>
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/3bcbe410-26ca-4356-b03e-cee5cd64ab6b" width="32%"/>
  <img src="https://github.com/user-attachments/assets/de9e7539-32d6-48eb-9cf3-3aca1cce7728" width="32%"/>
  <img src="https://github.com/user-attachments/assets/653589c4-dbf2-45bb-a9e5-0d90f7b1a55c" width="32%"/>
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/3700cdc2-0cc4-426f-a8f8-b79971dbb458" width="49%"/>
  <img src="https://github.com/user-attachments/assets/4c753dca-163b-4fcb-b5cb-46cc3914f7b1" width="49%"/>
</p>



