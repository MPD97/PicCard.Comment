FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["src/PicCard.Comment.Api/PicCard.Comment.Api.csproj", "src/PicCard.Comment.Api/"]
RUN dotnet restore "src/PicCard.Comment.Api/PicCard.Comment.Api.csproj"
COPY . .
WORKDIR "/src/src/PicCard.Comment.Api"
RUN dotnet build "PicCard.Comment.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "PicCard.Comment.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "PicCard.Comment.Api.dll"]