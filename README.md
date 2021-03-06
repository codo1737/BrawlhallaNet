# Brawlhalla.Net
A .NET library to interact with the Brawlhalla API.

## Installation
Brawlhalla.Net is available from [NuGet](https://www.nuget.org/packages/Brawlhalla.Net).

Alternatively, you can install directly with `Install-Package Brawlhalla.NET`.

## Supported Frameworks
Brawlhalla.Net targets `netstandard1.4`, some examples of supported frameworks include:

.NET Core 1.1
.NET Framework 4.6.1+

## Example
```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;
// Import necessary usings
using BrawlhallaNet;
using BrawlhallaNet.Responses;

class Program
{
    // We need to create an async context in our main method
    public static void Main(string[] args) => MainAsync(args).GetAwaiter().GetResult();

    public static async Task MainAsync(string[] args)
    {
        var client = new BrawlhallaApiClient("API_KEY"); // Initialize our client, replace API_KEY with your api key

        // Configure our client's log feature
        client.Log += (sender, event) =>
        {
            Console.WriteLine(event.Message);
        };

        // Now we can start to make requests
        List<RankedPagePlayer> topPlayers = await client.GetRankedPageAsync("1v1", "all", 1);

        foreach (RankedPagePlayer player in topPlayers)
        {
            Console.WriteLine($"[{player.Rank}] {player.Name} ({player.ID}): {player.Elo}"); // Example output: [12] Boomie (257670): 2025
        }

        Clan bmg = await client.GetClanAsync(1);
        Console.WriteLine($"{bmg.Name} ({bmg.ClanCreationDate}): {bmg.Members.Count}"); // Blue Mammoth Games (5/25/2016 8:00:00 PM +00:00): 16

        var testPlayer = await client.GetRankedPlayerAsync(2);
        Console.WriteLine($"{testPlayer.Name} ({testPlayer.BrawlhallaId}): {testPlayer.Wins}/{testPlayer.Games}"); // [BMG] Dan (2): 2/2

        await Task.Delay(-1); // Pause our program until the user exits
    }
}
```

## Contributing
pls help

## Todo
- [x] Beta release 🎉 </br>
- [ ] Open issue with bugs </br>
- [ ] Open issue with planned features </br>
- [x] Push to NuGet 🎉 </br>
- [x] Start tests 🎉 </br>
- [ ] Xml comments for every method </br>

## Contact
Listed in order of how frequently I check them


Discord: Stereotypical Weeaboo#9990 (118971536395730946)

Reddit: /u/CallMeSometimeNever

Email: Steaboo@gmail.com
