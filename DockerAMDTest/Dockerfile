FROM mcr.microsoft.com/dotnet/runtime:7.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["DockerAMDTest/DockerAMDTest.csproj", "DockerAMDTest/"]
RUN dotnet restore "DockerAMDTest/DockerAMDTest.csproj"
COPY . .
WORKDIR "/src/DockerAMDTest"
RUN dotnet build "DockerAMDTest.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DockerAMDTest.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DockerAMDTest.dll"]
