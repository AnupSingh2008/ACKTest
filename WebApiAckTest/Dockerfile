#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["WebApiAckTest/WebApiAckTest.csproj", "WebApiAckTest/"]
RUN dotnet restore "WebApiAckTest/WebApiAckTest.csproj"
COPY . .
WORKDIR "/src/WebApiAckTest"
RUN dotnet build "WebApiAckTest.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebApiAckTest.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebApiAckTest.dll"]