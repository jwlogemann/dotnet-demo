FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["KubernetesDemo.csproj", "./"]
RUN dotnet restore "./KubernetesDemo.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "KubernetesDemo.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "KubernetesDemo.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "KubernetesDemo.dll"]
