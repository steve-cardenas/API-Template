#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 81
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["API-Template/API-Template.csproj", "API-Template/"]
RUN dotnet restore "API-Template/API-Template.csproj"
COPY . .
WORKDIR "/src/API-Template"
RUN dotnet build "API-Template.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "API-Template.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "API-Template.dll"]
