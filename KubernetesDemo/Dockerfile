FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY ["KubernetesDemo/KubernetesDemo.csproj", "KubernetesDemo/"]

RUN dotnet restore "KubernetesDemo/KubernetesDemo.csproj"
COPY . .
WORKDIR "/src/KubernetesDemo"
RUN dotnet build "KubernetesDemo.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "KubernetesDemo.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "KubernetesDemo.dll"]