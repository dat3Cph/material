---
title: Deployment Pipeline
description: Tutorial on how to deploy your project
layout: default
parent: Toolbox
nav_order: 5
has_children: true
permalink: /toolbox/deployment-pipeline/
---

# Deployment

På 2. semester deployede vi vores Javalin websites hos Digital Ocean. Vi gav to modeller. Den blå og den røde udgave. Den røde indbefattede køb af domænenavn. Nogle studerende har haft orlov, og har derfor ikke være igennem samme forløb. Så derfor skal du lige finde ud af hvilken kategori du hører til:

## Identificering af hvor lang vej du er kommet

| Kategori | Beskrivelse | What to do |
|---|---|----|
| A | Jeg har et domænenavn som styres via DNS hos Digital Ocean. |Perfekt. Ikke mere at gøre her|
| B | Jeg har ikke et domænenavn endnu |Du skal have købt et domænenavn, gerne et .dk domæne hos Dandomain og have redelegeret det til Digital Ocean. Hvis ikke du har gjort det endnu, så er der [en vejledning her](https://cphbusiness.cloud.panopto.eu/Panopto/Pages/Viewer.aspx?id=f8e7ebbb-8d17-480b-9ac2-b15600a699f2)|
| C | Jeg har en kørende Droplet hos Digital Ocean og vil gerne beholde den |Det er sådan set fint. Du har sikkert også en eller flere Javalin applikationer kørende. Hvis du stadig vil holde dem i luften, skal du være ekstra opmærksom når vi skal til at rode med `docker-compose.yml`. Der skal tilføjes en del nye ting, men du kan stadig beholde dine gamle opsætninger|
| D | Jeg har en kørende Droplet hos Digital Ocean og vil gerne starte forfra |Du kan 'destroye' den gamle Droplet med et snuptag hos Digital Ocean. Bagefter skal du følge vejledningerne nedenfor fra punkt 2|
| E | Jeg har ikke fået oprettet mig hos Digital Ocean endnu |Du skal bare starte fra begyndelsen. Dvs, punkt 0|
| F | Jeg har forsøgt at oprette mig hos Digital Ocean, men det er ikke lykkedes |Denne er lidt tricky.  Find først ud af om du evt. har anvendt en anden emailadresse end din **@cphbusiness.dk**. Det kan nemlig skabe problemer. Hvis det er tilfældet kan du evt. prøve at oprette dig fra starten med din **@cphbusiness.dk** mail. Hop til punkt 0. Hvis du tidligere har oprettet dig med din **@cphbusiness.dk** mail, skal du oprette en **support ticket** hos Digital Ocean og beskrive dit problem. Og når du har fået et ticket-nummer, skal du sende det til Jon|
| G | Jeg har en ssh-nøgle |Du er godt på vej. Hvis du ikke har en Droplet endnu, så hop til punkt 2|
| H | Jeg har ikke en ssh-nøgle |Du skal lige have oprettet en ssh-nøgle. Hop til punkt 1 og bagefter til punkt 0 eller hvor langt du nu er nået i processen|
| I | Jeg har Droplet, men jeg ved ikke rigtig om den virker som den skal |Vi anbefaler at du opretter en frisk Droplet og sletter den gamle. Vær opmærksom på at man betaler for hver Droplet man har liggende. Også selv den ikke kører. Så derfor er det billigst at slette den gamle i stedet for bare at stoppe den. Når den gamle er fjernet kan du gå til punkt 2|

## Oversigt over vejledninger

I forhold til ovenstående skema, kan du finde ud af hvad du mangler her:

0. [Opret dig hos Digital Ocean](./digitalocean_signup.md)
1. [Opret (eller find din) ssh nøgle](./sshkeys.md)
2. [Opsætning af virtuel server hos Digital Ocean](./droplet.md)
3. [Log på Droplet første gang](./logpaadroplet.md)
4. [Opret ny bruger i Ubuntu og konfigurer en firewall](./ubuntufix.md)
5. [Installation af Java 17 på Droplet](./java.md)
6. [Installation af Postgres 16.2 i en Docker container](./postgres_setup.md)
7. [Tag et snapshot af din Droplet](./snapshot.md)
8. [Deploy dit website (det gør vi først onsdag)](./docker_caddy_droplet.md)

Her er en oversigt over den overordnede system arkitektur:

![System](../deployment_infrastructure/images/systemarchitecture.png)

## Deployment Pipeline

Når du har fulgt ovenstående vejledninger, så er du klar til at deploye dit projekt. Vi har lavet en pipeline, som du kan følge.
