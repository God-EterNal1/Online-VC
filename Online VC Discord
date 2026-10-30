import nextcord
from nextcord.ext import commands
import base64, codecs
import os
import urllib.request

intents = nextcord.Intents.default()
intents.message_content = True
intents.voice_states = True
intents.guilds = True

bot = commands.Bot(command_prefix='!', help_command=None, intents=intents)

BotSever1 = 1562181928319189127  # ไอดี เซิฟเวอร์ดิสคอร์ด
BotSever2 = 1562181929258979401  # ไอดี ห้องที่จะให้บอทลง

@bot.event
async def on_ready():
    await bot.change_presence(activity=nextcord.Streaming(
        name="Phakaphop", url="https://www.twitch.tv/phakaphpop"))
    
    # เชื่อมต่อเข้าห้องเสียง
    try:
        channel = bot.get_channel(BotSever2)
        if channel and isinstance(channel, nextcord.VoiceChannel):
            if not channel.guild.voice_client:
                await channel.connect(self_deaf=True)
                print(f'Connected to voice channel: {channel.name}')
    except Exception as e:
        print(f'Error connecting to voice: {e}')
        
    print('Bot is ready.')

@bot.event
async def on_voice_state_update(member, before, after):
    # ระบบกันหลุด: ถ้าบอทหลุดออกจากห้องเสียง ให้มันต่อกลับเข้าไปเองอัตโนมัติ
    if member.id == bot.user.id:
        if before.channel and not after.channel:
            print('Bot was disconnected, trying to reconnect...')
            try:
                channel = bot.get_channel(BotSever2)
                if channel:
                    await channel.connect(self_deaf=True)
                    print('Reconnected successfully!')
            except Exception as e:
                print(f'Failed to reconnect: {e}')

    if after.channel and after.self_stream:
        print(f'{member.name} is in {after.channel.name} and started speaking.')

bot.run("MTUzNTMzNjUxNTU1MzcyMjM2OA.GNFnPK.noGlg_OHJJw0x9OyuzNbabLchHm4PyAfA-kV8I")
