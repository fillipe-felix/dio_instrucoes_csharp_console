FROM mcr.microsoft.com/dotnet/runtime:5.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["instrucoes/instrucoes.csproj", "instrucoes/"]
RUN dotnet restore "instrucoes/instrucoes.csproj"
COPY . .
WORKDIR "/src/instrucoes"
RUN dotnet build "instrucoes.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "instrucoes.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "instrucoes.dll"]
