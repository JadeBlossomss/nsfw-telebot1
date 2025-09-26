{\rtf1\ansi\ansicpg1252\cocoartf2822
\cocoatextscaling0\cocoaplatform0{\fonttbl\f0\fswiss\fcharset0 Helvetica;}
{\colortbl;\red255\green255\blue255;}
{\*\expandedcolortbl;;}
\margl1440\margr1440\vieww11520\viewh8400\viewkind0
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\f0\fs24 \cf0 import os, re, asyncio, aiosqlite\
from fastapi import FastAPI, Request, Header, HTTPException\
from aiogram import Bot, Dispatcher, types\
from aiogram.filters import Command\
\
BOT_TOKEN = os.getenv("BOT_TOKEN", "")\
APP_URL = os.getenv("APP_URL", "")\
WEBHOOK_SECRET = os.getenv("WEBHOOK_SECRET", "secret")\
MODE = os.getenv("MODE", "webhook")\
\
bot = Bot(token=BOT_TOKEN)\
dp = Dispatcher()\
app = FastAPI()\
\
RULES = (\
    "\uc0\u55357 \u56606  *Adults only (18+).* \\n"\
    "\uc0\u10060  No illegal/abusive content.\\n"\
    "\uc0\u55357 \u57003  No minors, bestiality, incest, non-consensual.\\n"\
    "Type /agree if you confirm."\
)\
\
BLOCK_REGEX = re.compile(r"(minor|under\\s*age|teen|rape|incest|bestiality)", re.I)\
\
async def init_db():\
    async with aiosqlite.connect("data.sqlite") as db:\
        await db.execute("CREATE TABLE IF NOT EXISTS users (id INTEGER PRIMARY KEY, agreed INT)")\
        await db.commit()\
\
async def set_agreed(uid): \
    async with aiosqlite.connect("data.sqlite") as db:\
        await db.execute("INSERT OR REPLACE INTO users VALUES (?,1)", (uid,))\
        await db.commit()\
\
async def is_agreed(uid):\
    async with aiosqlite.connect("data.sqlite") as db:\
        async with db.execute("SELECT agreed FROM users WHERE id=?", (uid,)) as c:\
            row = await c.fetchone()\
            return bool(row)\
\
@dp.message(Command("start"))\
async def start(m: types.Message):\
    await m.answer(RULES, parse_mode="Markdown")\
\
@dp.message(Command("agree"))\
async def agree(m: types.Message):\
    await set_agreed(m.from_user.id)\
    await m.answer("\uc0\u9989  Verified. Type /menu to begin.")\
\
@dp.message(Command("menu"))\
async def menu(m: types.Message):\
    if not await is_agreed(m.from_user.id):\
        return await m.answer("Please /start and /agree first.")\
    await m.answer("What vibe are you in the mood for?")\
\
@dp.message()\
async def chat(m: types.Message):\
    if not await is_agreed(m.from_user.id):\
        return await m.answer("Please /start and /agree first.")\
    if BLOCK_REGEX.search(m.text or ""):\
        return await m.answer("\uc0\u55357 \u57003  Not allowed.")\
    await m.answer("\uc0\u55357 \u56492  [Adult but safe reply here]")\
\
@app.on_event("startup")\
async def on_start():\
    await init_db()\
    if MODE == "webhook" and APP_URL:\
        await bot.set_webhook(url=f"\{APP_URL\}/telegram", secret_token=WEBHOOK_SECRET)\
\
@app.post("/telegram")\
async def webhook(request: Request, x_telegram_bot_api_secret_token: str = Header(None)):\
    if x_telegram_bot_api_secret_token != WEBHOOK_SECRET:\
        raise HTTPException(403, "Forbidden")\
    update = await request.json()\
    await dp.feed_webhook_update(bot, update)\
    return \{"ok": True\}\
\
@app.get("/")\
async def health():\
    return \{"ok": True\}\
}