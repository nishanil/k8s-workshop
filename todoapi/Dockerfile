FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 58604
EXPOSE 44341

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY todoapi/todoapi.csproj todoapi/
RUN dotnet restore todoapi/todoapi.csproj
COPY . .
WORKDIR /src/todoapi
RUN dotnet build todoapi.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish todoapi.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "todoapi.dll"]
