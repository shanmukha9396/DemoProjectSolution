# Use the offical .Net Core SDK image as the base image
FROM mcr.microsoft.com/dotnet/sdk:8.0 as build
WORKDIR /app

#Copy the project file and restore dependencies (use .csproj for the Project name)
COPY *.csproj ./
RUN dotnet restore

# Copy the rest of the application code
COPY . .

# Publish the application
RUN dotnet publish -c Release -o out

# Build the runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 as runtime
WORKDIR /app
COPY --from=build /app/out ./

# Expose the port that the application will run on
EXPOSE 80

# Start the application
ENTRYPOINT ["dotnet", "MyDemoProject.dll"]