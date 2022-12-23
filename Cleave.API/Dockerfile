FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY [".", "Cleave.API/"]
RUN dotnet restore "Cleave.API/Cleave.API.csproj"
COPY . .
WORKDIR "/src/Cleave.API"
RUN dotnet build "Cleave.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Cleave.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Cleave.API.dll"]
