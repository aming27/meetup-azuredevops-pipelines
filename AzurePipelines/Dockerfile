FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
#COPY ./*.sln ./
COPY . .


RUN dotnet restore
COPY . .

FROM build AS publish
WORKDIR /src
RUN dotnet publish -c Release  -o /app 

FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS run
WORKDIR /app
COPY --from=publish /app ./
ENTRYPOINT ["dotnet", "AzurePipelines.dll"]
