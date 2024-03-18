# Use the .NET SDK image to build the application
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build-env
WORKDIR /app

# Copy the csproj and restore any dependencies (via NuGet)
COPY MyDotNetApp/MyDotNetApp.csproj ./
RUN dotnet restore

# Copy the project files and build the release
COPY MyDotNetApp/ ./
RUN dotnet publish -c Release -o out

# Generate the runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build-env /app/out .
EXPOSE 8080

# Set the environment variable to listen on port 8080
ENV ASPNETCORE_URLS=http://*:8080

ENTRYPOINT ["dotnet", "MyDotNetApp.dll"]
