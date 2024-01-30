---
title: Day 3 C Sharp practice - Web API
tags:
---
Before diving into our ultimate goal, some foundational knowledge is required.
Today I will do a practice for building a simple .Net WEB API.

Create a new project
![[Pasted image 20240129215619.png]]

Search "API" -> select ASP. NET Core Web API -> Next
![[Pasted image 20240129215803.png]]

Input project name "CustomerAPI" -> Next
![[Pasted image 20240129220024.png]]

Select .Net 8.0 (Long Term Support) -> Create
![[Pasted image 20240129220140.png]]

After creating the project, we can see visiual studio have already help us to generate some template files.
![[Pasted image 20240129221608.png]]

| File name |  |
| ---- | ---- |
| launchSettings.json | project setting file |
| Program.cs | Main program file |
| CustomerAPI.http | Default http file |
Now, we can test our project is work or not, simply press the start button (without debugging)
![[Pasted image 20240129223008.png]]

A Swagger page will show up
![[Pasted image 20240129223258.png]]

We can check the respones data here
![[Pasted image 20240129224001.png]]

If not, I suggest go to chrome://flags/,
to Enable the "Allow invalid certificates for resources loaded from localhost".
To allow browser access the localhost resource without certificates.
![[Pasted image 20240129223618.png]]

Or you can put the link `{@CustomerAPI_HostAddress}/WeatherForecast` to the search bar of the browser or Postman

![[Pasted image 20240129224317.png]]

![[Pasted image 20240129224350.png]]

For the request link, you can copy it from swagger
![[Pasted image 20240129224516.png]]

or go to `launchSettings.json` to find out the `{@CustomerAPI_HostAddress}
under "profiles ->https"
![[Pasted image 20240129224910.png]]

We will our own date for API tomorrow. 