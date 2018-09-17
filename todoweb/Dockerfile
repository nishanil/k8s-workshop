FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 3010
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY todoweb/todoweb.csproj todoweb/
RUN dotnet restore todoweb/todoweb.csproj
COPY . .
WORKDIR /src/todoweb
RUN dotnet build todoweb.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish todoweb.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "todoweb.dll"]
