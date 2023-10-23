# docker build -t azureopenai.azurecr.io/azureopenaibot -f 'webapi/Dockerfile' .
# docker push azureopenai.azurecr.io/azureopenaibot

FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80

#ENV ASPNETCORE_URLS=http://localhost:80
ENV ASPNETCORE_ENVIRONMENT=Production

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["webapi/nuget.config", "webapi/"]
COPY ["webapi/CopilotChatWebApi.csproj", "webapi/"]
COPY ["shared/CopilotChatShared.csproj", "shared/"]
RUN dotnet restore "webapi/CopilotChatWebApi.csproj"
COPY . .
WORKDIR "/src/webapi"
RUN dotnet build "CopilotChatWebApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CopilotChatWebApi.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CopilotChatWebApi.dll"]