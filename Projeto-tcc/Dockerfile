#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["TCC-2.0/TCC-2.0.csproj", "TCC-2.0/"]
RUN dotnet restore "TCC-2.0/TCC-2.0.csproj"
COPY . .
WORKDIR "/src/TCC-2.0"
RUN dotnet build "TCC-2.0.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TCC-2.0.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
RUN useradd -m tccfinal

USER tccfinal

CMD ASPNETCORE_URLS="https://*:$PORT dotnet TCC-2.0"