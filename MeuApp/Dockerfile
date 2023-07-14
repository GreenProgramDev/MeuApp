FROM mcr.microsoft.com/dotnet/runtime:7.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["MeuApp/MeuApp.csproj", "MeuApp/"]
RUN dotnet restore "MeuApp/MeuApp.csproj"
COPY . .
WORKDIR "/src/MeuApp"
RUN dotnet build "MeuApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MeuApp.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MeuApp.dll"]
