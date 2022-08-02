#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["DevCashBack.WebApi/DevCashBack.WebApi.csproj", "DevCashBack.WebApi/"]
RUN dotnet restore "DevCashBack.WebApi/DevCashBack.WebApi.csproj"
COPY . .
WORKDIR "/src/DevCashBack.WebApi"
RUN dotnet build "DevCashBack.WebApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DevCashBack.WebApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DevCashBack.WebApi.dll"]