#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/runtime:5.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["ConsoleHelloWorld5/ConsoleHelloWorld5.csproj", "ConsoleHelloWorld5/"]
RUN dotnet restore "ConsoleHelloWorld5/ConsoleHelloWorld5.csproj"
COPY . .
WORKDIR "/src/ConsoleHelloWorld5"
RUN dotnet build "ConsoleHelloWorld5.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ConsoleHelloWorld5.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ConsoleHelloWorld5.dll"]