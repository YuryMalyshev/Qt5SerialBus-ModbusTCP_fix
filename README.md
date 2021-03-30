# Qt5SerialBus-ModbusTCP_fix
For: Qt 5.15.2
A simple fix which allows ModbusTCP handle my custom commands.


How to add new custom commands:
1. Add the command to "enum FunctionCode" in "qmodbuspdu.h" file
2. Add minimum data size case for the command to a switch case in "static int minimumDataSize(const QModbusPdu &pdu, Type type)" function inside of "qmodbuspdu.cpp".
3. Register data size calculator inside your main:
```c++
QModbusResponse::registerDataSizeCalculator(QModbusPdu::FunctionCode(custom_fun_code), [](const QModbusResponse &)-> int
{
    return 42;
});
```
(4. Build Qt. The resulting dll (on Windows) will be in <build dir>\qtbase\bin)


To build Qt follow the instructions from here: [GitHub - Qt5](https://github.com/qt/qt5/tree/5.15.2)

Sometimes the compilation might result in an error (tested on Windows10). Adding **-opengl desktop** parameter to "configuration" might help.
