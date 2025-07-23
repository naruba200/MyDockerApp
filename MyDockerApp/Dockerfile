# Base image để chạy ứng dụng
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80

# Stage build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["MyDockerApp.csproj", "./"]
RUN dotnet restore "./MyDockerApp.csproj"
COPY . .
RUN dotnet publish "MyDockerApp.csproj" -c Release -o /app/publish

# Runtime stage
FROM base AS final
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "MyDockerApp.dll"]

# Chỉ dùng runtime image (đã publish rồi)
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
EXPOSE 3000
COPY ./publish ./
ENTRYPOINT ["dotnet", "P27625.dll"]
