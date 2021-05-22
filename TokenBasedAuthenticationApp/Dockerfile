#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["TokenBasedAuthenticationApp/TokenBasedAuthenticationApp.csproj", "TokenBasedAuthenticationApp/"]
RUN dotnet restore "TokenBasedAuthenticationApp/TokenBasedAuthenticationApp.csproj"
COPY . .
WORKDIR "/src/TokenBasedAuthenticationApp"
RUN dotnet build "TokenBasedAuthenticationApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TokenBasedAuthenticationApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TokenBasedAuthenticationApp.dll"]