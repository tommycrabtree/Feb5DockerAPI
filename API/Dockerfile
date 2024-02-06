# Get a base SDK Image from Microsoft
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build-env
WORKDIR /App

# Copy everything, including the .csproj file, and restore any dependencies via NuGet
COPY . ./

# Restore as distinct layers
RUN dotnet restore

# Build and publish a release
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:7.0
WORKDIR /App
EXPOSE 80
COPY --from=build-env /App/out .
ENTRYPOINT [ "dotnet", "API.dll" ]
