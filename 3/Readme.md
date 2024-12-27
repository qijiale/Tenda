## Tenda AC18 stack overflow vulnerability

## 1. Affected version
V15.03.05.19

## 2. Vulnerability details
   In the function form_fast_setting_wifi_set handling the "ssid" parameter  in httpd , it assigns the value obtained from the sub_2BA8C function to the src variable and checks if it is non-empty. If non-empty, the program directly copies the content of src into two stack buffers, s and dest, using the strcpy function. However, no size validation is performed on the content of src before the copying operation.
Since strcpy does not limit the length of the copied data, an attacker can supply a crafted "ssid" parameter with a length exceeding the size of the stack buffers (s and dest, each 64 bytes), leading to a stack-based buffer overflow. This vulnerability can result in Denial of Service (DoS) or potentially allow an attacker to achieve Remote Code Execution (RCE) by overwriting critical stack memory with controlled data.

   ![My Image](1.png)


