FROM mcr.microsoft.com/dotnet/runtime:5.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["PlaywrightTests/PlaywrightTests.csproj", "PlaywrightTests/"]
RUN dotnet restore "PlaywrightTests/PlaywrightTests.csproj"
COPY . .
WORKDIR "/src/PlaywrightTests"
RUN dotnet build "PlaywrightTests.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "PlaywrightTests.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "PlaywrightTests.dll"]
