#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Oink.UserMgmt.Profile/Oink.UserMgmt.Profile.csproj", "Oink.UserMgmt.Profile/"]
RUN dotnet restore "Oink.UserMgmt.Profile/Oink.UserMgmt.Profile.csproj"
COPY . .
WORKDIR "/src/Oink.UserMgmt.Profile"
RUN dotnet build "Oink.UserMgmt.Profile.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Oink.UserMgmt.Profile.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Oink.UserMgmt.Profile.dll"]