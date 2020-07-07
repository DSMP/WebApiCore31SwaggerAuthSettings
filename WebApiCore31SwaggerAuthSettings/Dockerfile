#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["WebApiCore31SwaggerAuthSettings/WebApiCore31SwaggerAuthSettings.csproj", "WebApiCore31SwaggerAuthSettings/"]
RUN dotnet restore "WebApiCore31SwaggerAuthSettings/WebApiCore31SwaggerAuthSettings.csproj"
COPY . .
WORKDIR "/src/WebApiCore31SwaggerAuthSettings"
RUN dotnet build "WebApiCore31SwaggerAuthSettings.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebApiCore31SwaggerAuthSettings.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebApiCore31SwaggerAuthSettings.dll"]