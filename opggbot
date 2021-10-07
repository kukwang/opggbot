# ********************************************************************************
# opgg_bot.py
# Using selenium library
# ********************************************************************************

import nest_asyncio
import aiohttp
import discord
import selenium
from selenium import webdriver
from discord.ext import commands

nest_asyncio.apply()
webdriver_options = webdriver.ChromeOptions()
webdriver_options.add_argument('headless')
driver = webdriver.Chrome(executable_path='chromedriver', options=webdriver_options)

bot = commands.Bot(command_prefix='옵지 ', connector=aiohttp.TCPConnector(ssl=False))
Token = 'Nzg2ODI1MDI3MTg1NDEwMDY4.X9MB6A.QvoLoqG2D4JJqKdX52paUlDZsMQ'

@bot.event
async def on_ready():
    print('Bot connected')

# '옵지 승률 '닉넴''을 치면 '닉넴'의 승률을 출력
@bot.command()
async def 승률(ctx, arg):
    # get address
    driver.get(url='https://www.op.gg/summoner/userName='+arg)
    
    # xpath 사용해서 찾음
    win_lose = driver.find_element_by_xpath("//*[@id=\"GameAverageStatsBox-summary\"]/div[1]/table/tbody/tr[1]/td[1]/div/span[1]").text
    win_rate = driver.find_element_by_xpath("//*[@id=\"GameAverageStatsBox-summary\"]/div[1]/table/tbody/tr[2]/td[1]/div/div[2]").text

    await ctx.send('{}의 최근 {}판 승률은 {}입니다'.format(arg, win_lose, win_rate))


# '옵지 모스트 '닉넴''을 치면 이번시즌 '닉넴'의 모스트 챔프를 출력
@bot.command()
async def 모스트(ctx, arg):
    # get address
    driver.get(url='https://www.op.gg/summoner/userName='+arg)
    
    # xpath 사용해서 찾음
    most = driver.find_element_by_xpath("//*[@id=\"SummonerLayoutContent\"]/div[2]/div[1]/div[3]/div[2]/div[1]/div/div[1]/div[2]/div[1]/a").text    

    await ctx.send('이번시즌 {}의 모스트는 {}입니다'.format(arg, most))
    
# '옵지 나가'를 치면 logout함
@bot.command()
async def 나가(ctx):
    await ctx.send('잘있어요')
    await ctx.bot.change_presence(status=discord.Status.offline)
    await ctx.bot.logout()
    print("Bot disconnected")
    
bot.run(Token)
