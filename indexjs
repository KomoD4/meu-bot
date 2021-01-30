const express = require('express');
const app = express();
app.get("/", (request, response) => {
  const ping = new Date();
  ping.setHours(ping.getHours() - 3);
  console.log(`Ping recebido às ${ping.getUTCHours()}:${ping.getUTCMinutes()}:${ping.getUTCSeconds()}`);
  response.sendStatus(200);
});
app.listen(process.env.PORT); // Recebe solicitações que o deixa online

const Discord = require("discord.js"); //Conexão com a livraria Discord.js
const client = new Discord.Client(); //Criação de um novo Client
const config = require("./config.json"); //Pegando o prefixo do bot para respostas de comandos
const discord = require("discord.js");
const nuke = new discord.Client();




client.on("message", async message => {
  const regex = /(https?:\/\/)?(www\.)?(discord\.(gg|io|me|li|club)|discordapp\.com\/invite|discord\.com\/invite)\/.+[a-z]/gi;
  if (regex.exec(message.content)) {
    await message.delete({timeout: 1000});
      await message.channel.send(
        `${message.author} **você não pode postar link de outros servidores aqui!**`
      );
  }
});;


client.on("guildMemberRemove", async (member) => { 

  let guild = await client.guilds.cache.get("805144167721467925");
  let channel = await client.channels.cache.get("805183047627440138");
  let emoji = await member.guild.emojis.cache.find(emoji => emoji.name === "nomedoemoji");
  if (guild != member.guild) {
    return console.log("");
   } else {
      let embed = await new Discord.MessageEmbed()
      .setColor("#7c2ae8")
      .setAuthor(member.user.tag, member.user.displayAvatarURL())
      .setTitle(` Adeus`)
      .setImage("https://pa1.narvii.com/6504/0ff90c7b09278234299fd2ef37d1eda4f27946d7_hq.gif")
      .setDescription(`**${member.user.username}**, Saiu do servidor :broken_heart:`)
      .setThumbnail(member.user.displayAvatarURL({ dynamic: true, format: "png", size: 1024 }))
      .setFooter("")
      .setTimestamp();

    channel.send(embed);
  }
});

client.on("guildMemberAdd", async (member) => { 

  let guild = await client.guilds.cache.get("805144167721467925");
  let channel = await client.channels.cache.get("805183047627440138");
  let emoji = await member.guild.emojis.cache.find(emoji => emoji.name === "nomedoemoji");
  if (guild != member.guild) {
    return console.log("");
   } else {
      let embed = await new Discord.MessageEmbed()
      .setColor("#7c2ae8")
      .setAuthor(member.user.tag, member.user.displayAvatarURL())
      .setTitle(` Boas-vindas`)
      .setImage("https://th.bing.com/th/id/Rc2ce2d82a11c90b05ad4abd796ef2fff?rik=KbfBjIDOTXhn5Q&riu=http%3a%2f%2fgifimage.net%2fwp-content%2fuploads%2f2017%2f09%2fanime-waving-gif-4.gif&ehk=vbF00Xm8Woqb05BN%2bLBaxy8IeV274tMydxR2iBZF9g8%3d&risl=&pid=ImgRaw")
      .setDescription(`**${member.user}**,Seja bem-vindo(a) ao servidor **${guild.name}**. Atualmente estamos com **${member.guild.memberCount} membros**, Espero que se divetar :heart:`)
      .setThumbnail(member.user.displayAvatarURL({ dynamic: true, format: "png", size: 1024 }))
      .setFooter("")
      .setTimestamp();

    channel.send(embed);
  }
});


client.on("ready", () => {
  let activities = [
      `Utilize ${config.prefix}help para obter ajuda`,
      `${client.guilds.cache.size} servidores!`,
      `${client.channels.cache.size} canais!`,
      `${client.users.cache.size} usuários!`
    ],
    i = 0;
  setInterval( () => client.user.setActivity(`${activities[i++ % activities.length]}`, {
        type: "WATCHING"
      }), 1000 * 60); 
  client.user
      .setStatus("dnd")
      .catch(console.error);
console.log("Estou Online!")
});


client.on('message', message => {
     if (message.author.bot) return;
     if (message.channel.type == 'dm') return;
     if (!message.content.toLowerCase().startsWith(config.prefix.toLowerCase())) return;
     if (message.content.startsWith(`<@!${client.user.id}>`) || message.content.startsWith(`<@${client.user.id}>`)) return;

    const args = message.content
        .trim().slice(config.prefix.length)
        .split(/ +/g);
    const command = args.shift().toLowerCase();


    try {
        const commandFile = require(`./commands/${command}.js`)
        commandFile.run(client, message, args);
    } catch (err) {
    console.error('Erro:' + err);
  }
});


client.login(process.env.TOKEN); //Ligando o Bot caso ele consiga acessar o token
