#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet-alpine:5.0 AS base
WORKDIR /app
EXPOSE 5000
EXPOSE 5001

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["NeuronNetwork.Site/NeuronNetwork.Site.csproj", "NeuronNetwork.Site/"]
RUN dotnet restore "NeuronNetwork.Site/NeuronNetwork.Site.csproj"
COPY . .
WORKDIR "/src/NeuronNetwork.Site"
RUN dotnet build "NeuronNetwork.Site.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "NeuronNetwork.Site.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "NeuronNetwork.Site.dll"]