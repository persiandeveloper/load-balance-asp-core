FROM mcr.microsoft.com/dotnet/core/sdk:3.1-alpine AS build
WORKDIR /app

COPY ./*.csproj ./
RUN dotnet restore

COPY . .
RUN dotnet build

RUN dotnet publish -c Release -o /out --no-restore


FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-alpine AS runtime
WORKDIR /app
COPY --from=build /out ./
ENV ASPNETCORE_URLS http://*:5000
ENTRYPOINT ["dotnet", "TodoApi.dll"]