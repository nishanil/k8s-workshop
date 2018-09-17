FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 58604
EXPOSE 44341

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY k8s-todo-api/k8s-todo-api.csproj k8s-todo-api/
RUN dotnet restore k8s-todo-api/k8s-todo-api.csproj
COPY . .
WORKDIR /src/k8s-todo-api
RUN dotnet build k8s-todo-api.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish k8s-todo-api.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "k8s-todo-api.dll"]
