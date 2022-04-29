- c/c++编译器

  https://github.com/mstorsjo/llvm-mingw/releases，下载llvm-mingw-20220323-msvcrt-x86_64.zip，解压并将编译器路径调整为“{LLVM_PATH}\bin\x86_64-w64-mingw32-gcc.exe”

- c/c++包管理

  vcpkg，将`${vcpkgRoot}/installed/x64-windows/include`添加到

- 工作区增加pylance解析时寻找范围：在工作区的.vscode/settings.json中添加如下项

  ```json
  {
      "python.analysis.extraPaths": [
          "/data/workspace/yuzijian/yolor",
          "/data/workspace/yuzijian/OC_SORT"
        ]
  }
  ```

  