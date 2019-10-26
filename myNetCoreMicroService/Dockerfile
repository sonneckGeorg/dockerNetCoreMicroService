FROM mcr.microsoft.com/dotnet/core/sdk:3.0 AS build 
# relative adds and copys uses this workdir in image
WORKDIR /src  
# csproj is copied to /src
COPY myNetCoreMicroService.csproj . 
# restores dependencies in image and create a new layer
RUN dotnet restore 
# copies all from source to WORKDIR in image (omitting already existing files)
COPY . . 
# -c (configuration: release), -o (output diretory) -> in this case absolute /app
RUN dotnet publish -c release -o /app 

FROM mcr.microsoft.com/dotnet/core/aspnet:3.0
WORKDIR /app
COPY --from=build /app .
ENTRYPOINT ["dotnet", "myNetCoreMicroService.dll"]