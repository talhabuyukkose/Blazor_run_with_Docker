#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app

EXPOSE 5281


ENV ASPNETCORE_URLS=http://+:5281

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["TestApp.UI/TestApp.UI.csproj", "TestApp.UI/"]
RUN dotnet restore "TestApp.UI/TestApp.UI.csproj"
COPY . .
WORKDIR "/src/TestApp.UI"
RUN dotnet build "TestApp.UI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TestApp.UI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TestApp.UI.dll"]