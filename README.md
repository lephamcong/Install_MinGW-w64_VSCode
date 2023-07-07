# Hướng dẫn cài đặt MinGW-w64 trên **Visual Studio Code** (VSCode)

Hướng dẫn này cung cấp các bước chi tiết để cài đặt MinGW-w64 trên Windows và cấu hình nó để phát triển ứng dụng C/C++ trên **Visual Studio Code** (VS Code). Tuy nhiên bạn có thể sử dụng ***DEV-C++*** thay cho VSCode, nó đơn giản hơn rất nhiều.

## YÊU CẦU TRƯỚC KHI CÀI ĐẶT:
## Trước khi bắt đầu, đảm bảo bạn đã có các điều kiện sau:

* Hệ điều hành Windows
* Đã cài đặt **Visual Studio Code** (VS Code) (Tải về tại đây: https://code.visualstudio.com/)
* Kết nối internet ổn định

## CÁC BƯỚC CÀI ĐẶT:
### Bước 1: Tạo một file Cpp mẫu trên *VS Code*
1. Mở hoặc tạo một thư mục trống trên máy tính
2. Mở một file C++ có sẵn hoặc tạo một file đơn giản **hello_world.cpp** như sau:
   ```cpp
    #include <iostream>
    int main() {
      std::cout << "Hello, World!" << std::endl;
      return 0;
    }
   ```
3. Cài đặt các Extension cần thiết cho C/C++ trên VS Code
   ![image](https://github.com/lephamcong/Install_MinGW-w64_VSCode/assets/80463984/37148adc-37b4-4b9d-8cc0-4ec1bedefe2c)
4. Cài đặt C/C++ Compiler:
   * *C/C++ Extension* không bao gồm trình *C/C++ Compiler*. Vì vậy, bạn sẽ cần cài đặt *C/C++ Compiler* hoặc sử dụng trình biên dịch đã được cài đặt sẵn trên máy tính của bạn.
   * Window: Bạn có thể tải từ Repository này sau đó giải nén vào thư mục C (không bao gồm file README.md). Hoặc tải từ https://github.com/gorvgoyl/MinGW64/releases (file MinGW64.zip). Lưu ý cần đảm bảo thêm *C/C++ Complier* vào ***System Path*** trên máy tính của bạn (tham khảo bên dưới)!!!
   * Với MacOS: Tham khảo https://developer.apple.com/xcode/
   * Với Linux: Tham khảo https://gcc.gnu.org/
5. Thêm *C/C++ Compiler* vào ***System path***: 
   * Tìm đường dẫn của cài đặt MinGW-w64 trên máy tính của bạn. Thông thường, đường dẫn này sẽ là thư mục chứa trình biên dịch (gcc/g++) và các công cụ liên quan, ví dụ: "**C:\MinGW-w64\bin**".
   * Mở "**Control Panel**" trên Windows.
   * Tìm và mở "**System**" hoặc "**System and Security**" (tuỳ thuộc vào phiên bản Windows của bạn).
   * Chọn "**Advanced system settings**" (hoặc "**System Advanced Settings**").
   * Trong cửa sổ "**System Properties**", chọn tab "**Advanced**".
   * Ở phần "**Environment Variables**", chọn nút "**Environment Variables**".
   * Trong phần "**System Variables**", tìm và chọn biến có tên "**Path**", sau đó nhấp vào nút "**Edit**".
   * Trong cửa sổ "**Edit Environment Variable**", nhấp vào nút "**New**" để thêm một mục mới.
   * Nhập đường dẫn của thư mục MinGW-w64 (ví dụ: "**C:\MinGW-w64\bin**") vào ô văn bản và nhấp vào nút "**OK**".
   * Nhấp vào tất cả các nút "OK" hoặc "**Apply**" để lưu các thay đổi và đóng cửa sổ cấu hình.
6. Chạy và Debug C/C++:
   * Bạn sẽ nhận thấy rằng trong dự án mẫu của bạn cũng có một thư mục **.vscode**. Để cấu hình debug, hai tệp tin cần thiết là **launch.json** và **tasks.json** được yêu cầu nằm trong thư mục **.vscode**.
   * VSCode có thể tạo và tự động cấu hình các tệp tin này nếu chúng ta cố gắng debug lần đầu tiên. Để làm điều đó, hãy mở tệp tin C++ trong VSCode và nhấn F5 hoặc điều hướng đến **Debug -> Start Debugging** và chọn **C++ (GDB/LLDB)**, sau đó chọn **g++.exe** để build và debug file đang hoạt động.
  ![image](https://github.com/lephamcong/Install_MinGW-w64_VSCode/assets/80463984/9d976eb7-2966-4cdf-abea-3346aa27ab7e)
  ![image](https://github.com/lephamcong/Install_MinGW-w64_VSCode/assets/80463984/7ddec6cc-187c-49cf-9281-1d3ef3f23466)

   * Điều này sẽ tạo ra 2 tệp tin **launch.json** và **tasks.json** trong thư mục **.vscode** nhìn như dưới đây (cập nhật đường dẫn MinGW64 nếu không chính xác).
   * Chú ý rằng tôi đã thêm một cấu hình tùy chọn nữa là **g++ build & run active file** trong tệp tin **launch.json** và **g++ build & run** trong tệp tin **tasks.json** với mục đích chạy mã C/C++ mà không cần debug. Bây giờ bạn có thể lựa chọn cấu hình nào khi bạn bắt đầu debug. Bạn có thể loại bỏ các cấu hình mà bạn không cần.
     ![image](https://github.com/lephamcong/Install_MinGW-w64_VSCode/assets/80463984/aa128d92-bdd8-47d4-904e-edfc8ee62a9d)
  
   * **launch.json**
    ```json
    {
      "version": "0.2.0",
      "configurations": [
        {
          "name": "g++.exe build and debug active file",
          "type": "cppdbg",
          "request": "launch",
          "program": "${fileDirname}\\${fileBasenameNoExtension}.exe",
          "args": [],
          "stopAtEntry": false,
          "cwd": "${workspaceFolder}",
          "environment": [],
          "externalConsole": false,
          "MIMode": "gdb",
          "miDebuggerPath": "C:\\MinGW64\\bin\\gdb.exe",
          "setupCommands": [
            {
              "description": "Enable pretty-printing for gdb",
              "text": "-enable-pretty-printing",
              "ignoreFailures": true
            }
          ],
          "preLaunchTask": "g++.exe build active file"
        },
        {
          "name": "g++ build & run active file",
          "type": "cppdbg",
          "request": "launch",
          "program": "${fileDirname}\\${fileBasenameNoExtension}.exe",
          "args": [],
          "stopAtEntry": false,
          "cwd": "${workspaceFolder}",
          "environment": [],
          "externalConsole": false,
          "MIMode": "gdb",
          "miDebuggerPath": "C:\\MinGW64\\bin\\gdb.exe",
          "setupCommands": [
            {
              "description": "Enable pretty-printing for gdb",
              "text": "-enable-pretty-printing",
              "ignoreFailures": true
            }
          ],
          "preLaunchTask": "g++ build & run active file"
        }
      ]
    }
    
    
  * **tasks.json**
    ```json
    {
      "version": "0.2.0",
      "configurations": [
        {
          "name": "g++.exe build and debug active file",
          "type": "cppdbg",
          "request": "launch",
          "program": "${fileDirname}\\${fileBasenameNoExtension}.exe",
          "args": [],
          "stopAtEntry": false,
          "cwd": "${workspaceFolder}",
          "environment": [],
          "externalConsole": false,
          "MIMode": "gdb",
          "miDebuggerPath": "C:\\MinGW64\\bin\\gdb.exe",
          "setupCommands": [
            {
              "description": "Enable pretty-printing for gdb",
              "text": "-enable-pretty-printing",
              "ignoreFailures": true
            }
          ],
          "preLaunchTask": "g++.exe build active file"
        },
        {
          "name": "g++ build & run active file",
          "type": "cppdbg",
          "request": "launch",
          "program": "${fileDirname}\\${fileBasenameNoExtension}.exe",
          "args": [],
          "stopAtEntry": false,
          "cwd": "${workspaceFolder}",
          "environment": [],
          "externalConsole": false,
          "MIMode": "gdb",
          "miDebuggerPath": "C:\\MinGW64\\bin\\gdb.exe",
          "setupCommands": [
            {
              "description": "Enable pretty-printing for gdb",
              "text": "-enable-pretty-printing",
              "ignoreFailures": true
            }
          ],
          "preLaunchTask": "g++ build & run active file"
        }
      ]
    }
7. Khởi động lại VS Code
8. Chạy chương trình C/C++
  * Mở một tệp tin C/C++ bất kỳ, đặt một số breakpoints (hoặc không), và nhấn vào nút Play màu xanh lớn. (hoặc dùng phím **F5**)
  ![image](https://github.com/lephamcong/Install_MinGW-w64_VSCode/assets/80463984/a0ab95be-59b4-4ae8-87f7-342912ec0b2a)

## CHÚC BẠN CÀI ĐẶT THÀNH CÔNG!


