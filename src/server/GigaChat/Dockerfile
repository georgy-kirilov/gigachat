FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["./GigaChat.csproj", "./"]
RUN dotnet restore "GigaChat.csproj"
COPY . .
RUN dotnet build "GigaChat.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "GigaChat.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "GigaChat.dll"]