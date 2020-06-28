# dotnet trace

![source](https://channel9.msdn.com/Shows/On-NET/ASPNET-Core-Series-Tracing)

collects trace information from the os and base classes of your application.  you can further enhance this output by adding your own trace information, but the information out of the box is generally enough to resolve issues.

1. install the dotnet trace tool: `dotnet tool install -g dotnet-trace`
2. run the application you want to trace
3. list all running trace enabled processes: `dotnet trace ps`
4. trace the process: `dotnet trace collect -p <process id>`
5. when you are finished with tracing you will have a `.nettrace` file which can be viewed in **visual studio**.  alternatively, you can change this format to `speedscope` format and run it through `www.speedscope.app`: `dotnet trace convert trace.nettrace --format speedscope`
