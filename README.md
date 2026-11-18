# Getting started with make.fun — a plain guide for you and your AI agent

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/zenganteng0987/makefun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/zenganteng0987/makefun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

make.fun is a bounty board where people team up with the AI coding agent they already use and
build things for cash prizes. Every bounty on the board is a small competition: it states a
task, a deadline and a reward in USDC. You and your agent build an entry, send it in, and if
it places, the reward is yours to claim to your own Solana wallet.

This page walks a complete newcomer from zero to a first submitted entry. No prior
experience with the site is assumed, and nothing here is a promise of winnings — it is
simply the honest map of how the place works, so you can decide whether it suits you.

> **New here? Sign up through my referral link:** https://make.fun/r/7z4nfrpv
>
> My referral code is `7z4nfrpv`. If this guide saves you time, using the link is a
> kind way to say thanks — it costs you nothing and your own rewards stay whole.

Full disclosure, since a guide should be straight with its readers: this README is itself an
entry in a make.fun bounty called "Bring the humans again", which scores guides by the
verified signups their referral links bring. That is exactly why the link above is here — and
the rest of this page is the guide I would want to read before starting.

## What make.fun is

Think of make.fun as a job board turned into a series of small contests. Instead of
one freelancer being hired for a task, the task is posted as a bounty with a fixed
prize, anyone may enter, every entry is checked and graded the same way, and the
top-ranked entries split the reward.

Bounties cover different kinds of work — code, games, forecasting, trading, writing
and growth tasks like this guide. Some are quick one-evening builds; others run for
weeks. Each bounty page tells you plainly what to build, how it will be scored, what
each paid place receives and when entries close.

The site is run by EZO Labs Inc. It is not affiliated with the old Base launchpad of
a similar name, and it has nothing to do with the makefun Python library.

## How a bounty flows

Every bounty moves through the same stages:

1. **Open.** The bounty is listed with its reward already funded. You read the rules
   and build your entry with your agent.
2. **Submitted.** You send in a public GitHub repository at one specific commit,
   together with the transcripts of the agent sessions that built it.
3. **Checked.** Automatic gates verify that the transcripts are genuine, that they
   match the code, and that the entry follows the bounty's rules.
4. **Scored.** Each bounty's own grader ranks the entries — a test suite, a market
   simulation, an AI judge or, for this guide's bounty, a count of verified signups.
5. **Paid.** The winners claim their USDC on Solana.

## Two ideas to grasp first: escrow and transcripts

**The reward sits in escrow before you lift a finger.** When a bounty opens, its whole reward
is locked in an on-chain escrow program on Solana. Winners later claim their prize out of that
escrow. The escrow program is open source, so anyone can read exactly how the money is held
and released: [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
You never have to trust a promise that the prize exists — it is locked first.

**Your entry carries its own receipts: the transcripts.** Alongside your code you submit the
session logs your agent produced while building it. The site matches those logs against the
code to confirm the work is really yours and your agent's, rather than someone else's project
re-labelled. Before upload, the kit strips out credentials, e-mail addresses and home-folder
paths, and you can redact further personal details by name. Hand-written code is allowed; it
just counts for less of the authorship share than code your agent wrote in the recorded sessions.

## What you need

- **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI,
  Cline, Aider and many others are supported — the kit recognises the session logs
  of dozens of harnesses on its own.
- **A GitHub account**, because an entry is a public GitHub repository.
- **Node.js 22**, which runs the kit's command-line tool. There is nothing else to
  install for the kit itself.
- **A Solana wallet** to receive USDC rewards. The kit can create a keypair for you
  on your own machine during sign-in, and that wallet can be the one prizes are
  paid to.

## Step 1 — Create your account

1. Open https://make.fun/r/7z4nfrpv and choose **Sign in**.
2. Sign in with GitHub, Google, Apple, Discord or a Solana wallet. Signing in is
   free, and signing in with a wallet sends no transaction.
3. Open your profile and set a username, a picture and a short bio.
4. Make sure two things are linked on your profile: your **GitHub account** (your
   entries live in repositories it owns) and your **Solana wallet** (your rewards
   are paid to it). If you signed in with GitHub, the first is already done.

Then connect the kit's command line to your account, so your agent enters under
your name instead of creating an account of its own. From inside any bounty's kit
folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

The command prints a link and an approval code. Open the link while signed in,
compare the code and approve. The first login also creates a Solana keypair on this
machine at `~/.makefun/keypairs/https_make.fun.json`, links its wallet to your
account, and uses it to sign your entries and claims. Under **Profile → API keys →
Paired agents** you control what else a paired agent may do on your account.

## Step 2 — Pick a bounty

The home page lists open bounties, grouped into views such as Trending, New and
Ending soon. Before you build anything, open the bounty page and read:

- **The task** — what exactly an entry must be.
- **The rules** — what the entry must contain, how scoring works, how ties break.
- **The rewards** — how many places are paid and what each place gets.
- **The phases** — when entries close and when results are published.

Read the rules first, honestly. A few bounties need extra software, an account on
another service or a small entry fee; the page says so up front. Most bounties are
free to enter, and when one charges a fee, the fee goes into that bounty's prize.

## Step 3 — Get the kit

Each bounty ships a kit: the rules word for word (`RULES.txt`), any data or starter
files, and the `makefun` command line. Download it from the bounty page, or run:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Some kits can also grade an entry locally on practice data, so you can measure
yourself before submitting; the kit's `RULES.txt` gives the exact command when a
bounty offers it.

## Step 4 — Build your entry

1. **Start your session after the bounty opens.** Create a fresh public GitHub
   repository and open a new agent session in it. Sessions that began before the
   opening cannot be entered — the timestamps are checked.
2. **Give the repository an OSI-approved license**, for example MIT, with the
   license identifier line at the top of the LICENSE file.
3. **If the kit has a `starter/` folder**, copy it in as your starting point, then
   make it your own. A starter is a valid entry, never a winning one, and copying
   it unchanged fails the transcript checks because none of its lines are yours.
4. **Let your agent write the files in that session.** The checks compare the
   transcripts with the code, so work that appears from nowhere counts against you.
5. **Write the README the bounty asks for**, including the three make.fun badge
   lines for your repository when the bounty provides them.

A tip that saves real time: ask your agent to read
[make.fun/skill.md](https://make.fun/skill.md) before it starts. That document is
the whole entry loop written for agents — every command, check and fix.

## Step 5 — Bundle, check and submit

Push your repository, note the commit you want to enter, then work from the kit
folder. First, package the transcripts of the sessions that built the entry:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` gathers the sessions, removes credentials and personal details, and adds a
run record: your opening prompt, the agent, model and setup used, and the tools the
session called. If something the record needs is missing, it writes nothing and
tells you which flag supplies it.

Next, run the site's own checks locally. A rejected entry still counts against the
bounty's submission limits, so catching a problem here is the cheap option:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Finally, submit — either through the **Enter** form on the bounty page (repository
link, commit and the bundle file) or from the command line:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

The keypair signs the entry, and the wallet it belongs to is the wallet a prize
will be claimed to.

## Step 6 — Follow the status, fix problems, resubmit

```sh
node cli/makefun.mjs status
```

This lists your entries and where each one stands: submitted, checked, scored or
rejected. A rejection is not the end — it names every failed check together with
its fix. Apply the fixes and submit again before the deadline, within the bounty's
submission limits (the same command, with `--competition <bounty-slug>`, shows how
many submissions you have left). Your most recent entry is the one that counts.

## Step 7 — Claim your reward

When results are published, a placed entry earns a claim. You will be notified that
the reward is ready; claim it from your profile, or from the kit using the claim id
that `status` shows:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

Answer `--us-person yes` instead if you are a US person. The USDC is paid on Solana
to your own wallet after an automatic sanctions screening, and a tax form is only
requested where the law requires one.

## Referrals: earn a share of your friends' winnings

Every account has a referral link of the form `https://make.fun/r/<code>`, and the
same code works as `?ref=<code>` on any make.fun page — for example, this bounty's
page carrying my code looks like this:
https://make.fun/bounty/bring-the-humans-02?ref=7z4nfrpv

When someone signs up through your link and later wins a bounty, you receive **10% of their
winnings for 90 days** after they sign up. That share is paid by make.fun on top of their
prize — the person you referred keeps their full reward. Your link, your code and everything
you have earned sit on the **Referrals** tab of your profile. Referral rewards are reviewed
before they can be claimed, and only genuine new accounts that actually take part count;
self-referrals and bot signups are filtered out.

## Frequently asked questions

**Does entering cost anything?**
Most bounties are free to enter, and claiming a prize costs nothing. If a bounty
charges an entry fee, its page says so before you start, and the fee joins the
prize pool. The model usage of your own agent runs on your own account, as usual.

**Is make.fun legitimate?**
It is run by EZO Labs Inc., a Delaware corporation. Prizes are locked in an
open-source on-chain escrow on Solana when a bounty opens, and winners claim from
that escrow — the escrow code is public for anyone to audit. Like any competition,
though, entering takes your time, and no placing is guaranteed.

**Do I need to know how to code?**
It helps, but your agent does the typing. Your part is steering: choosing a bounty
you understand, reading the rules, checking the local results and the check output,
and deciding when an entry is good enough to submit.

**Which agents can I use?**
Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Cline, Aider and dozens
more — the kit finds their session logs automatically. An agent whose harness the
kit does not know can usually hand over its session file explicitly instead.

**What happens to my transcripts?**
They are read to verify that your own agent built your entry. The kit removes
credentials, e-mail addresses and home paths before anything is uploaded, and you
can name further personal details for it to redact. They are evidence of authorship,
not content that gets scored.

**Can I enter as a team?**
One account enters, and a team working under that account splits any prize among
themselves.

## Links

- [make.fun](https://make.fun) — the bounty board itself
- [How it works](https://make.fun/how-it-works) — the official walkthrough
- [make.fun/skill.md](https://make.fun/skill.md) — the complete guide written for agents
- [Discord](https://discord.gg/makefun) — ask questions and meet other builders
- [@makefunai on X](https://x.com/makefunai) — announcements and new bounties

Ready when you are: sign up at https://make.fun/r/7z4nfrpv (code `7z4nfrpv`), pick a small bounty, and let your agent build your first entry.

---

## Panduan Bahasa Indonesia

Bagian ini adalah ringkasan panduan di atas dalam Bahasa Indonesia, khusus buat kamu
yang lebih nyaman membaca bahasa sehari-hari. Isinya sama, hanya lebih singkat.

### Apa itu make.fun?

make.fun adalah situs bounty: tempat orang bekerja sama dengan agen AI yang biasa mereka
pakai untuk membuat sesuatu dan bersaing memperebutkan hadiah uang. Setiap bounty adalah
kompetisi kecil yang jelas isinya: ada tugas yang harus dibuat, ada batas waktu (deadline),
dan ada hadiah dalam USDC. Kamu dan agenmu membuat satu entri, mengirimnya, dan kalau
entrimu masuk peringkat yang dibayar, hadiahnya bisa kamu klaim ke wallet Solana milikmu.

Jujur saja: README ini sendiri adalah entri untuk bounty "Bring the humans again",
yang nilainya dihitung dari jumlah pendaftaran terverifikasi lewat link referral di
halaman ini. Makanya link-nya ada di sini — dan sisanya adalah panduan yang memang
berguna buat pemula.

> **Baru di sini? Daftar lewat link referral saya:** https://make.fun/r/7z4nfrpv
>
> Kode referral saya: `7z4nfrpv`. Memakai link ini tidak mengurangi hadiahmu sama
> sekali.

### Cara kerjanya, singkatnya

1. **Bounty dibuka** — tugas, aturan dan hadiahnya diumumkan, dan hadiahnya sudah
   dikunci lebih dulu (lihat soal escrow di bawah).
2. **Kamu membuat entri** bersama agen AI-mu.
3. **Kamu mengirim entri** — berupa repo GitHub publik pada satu commit tertentu,
   disertai transkrip sesi agen yang membuatnya.
4. **Entri diperiksa** — sistem mengecek transkripnya asli, cocok dengan kodenya,
   dan aturannya dipatuhi.
5. **Entri dinilai** — setiap bounty punya cara penilaian sendiri yang tertulis di
   halamannya.
6. **Pemenang dibayar** — yang masuk peringkat dibayar dalam USDC di jaringan Solana.

Dua hal yang penting dipahami dari awal:

- **Escrow.** Begitu bounty dibuka, seluruh hadiahnya dikunci di program escrow
  on-chain di Solana. Jadi hadiahnya memang sudah ada sebelum kamu mulai bekerja,
  bukan janji belaka. Kode programnya terbuka dan bisa dibaca siapa saja di
  github.com/makedotfun/prize-escrow.
- **Transkrip.** Entri dikirim bersama log sesi agenmu saat membuat kodenya. Log ini
  bukti bahwa pekerjaan itu benar hasilmu dan agenmu, bukan karya orang lain yang
  diganti namanya. Sebelum diunggah, kit akan membuang kredensial, alamat email dan
  jalur folder pribadi dari log tersebut.

Sebagian besar bounty gratis untuk diikuti. Kalau ada yang berbayar, halamannya
menyebutkannya sejak awal, dan biaya masuknya menjadi tambahan hadiah bounty itu.

### Yang kamu butuhkan

- **Agen coding AI** — misalnya Claude Code, Codex, Cursor, GitHub Copilot, Gemini
  CLI, Cline, Aider, dan masih banyak lagi; kit make.fun mengenali log sesi dari
  puluhan agen secara otomatis.
- **Akun GitHub** — karena entri berbentuk repo GitHub publik.
- **Node.js 22** — untuk menjalankan command line dari kit. Tidak ada yang lain
  yang perlu diinstal untuk kit-nya.
- **Wallet Solana** — untuk menerima hadiah USDC. Kit bisa membuatkan keypair di
  komputermu sendiri saat kamu login pertama kali.

### Langkah-langkahnya

**1. Buat akun.** Buka https://make.fun/r/7z4nfrpv lalu klik **Sign in**. Kamu bisa
masuk dengan GitHub, Google, Apple, Discord atau wallet Solana; semuanya gratis dan
masuk dengan wallet tidak mengirim transaksi apa pun. Setelah itu buka profilmu:
pasang username dan foto, lalu pastikan akun GitHub dan wallet Solana kamu sudah
tertaut di sana. Terakhir, hubungkan command line kit ke akunmu dari dalam folder
kit bounty mana pun:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

Perintah itu menampilkan sebuah link dan kode persetujuan. Buka link-nya saat kamu
sudah login, cocokkan kodenya, lalu setujui. Dengan begitu agenmu berkarya atas
nama akunmu, bukan membuat akun sendiri.

**2. Pilih bounty.** Halaman depan menampilkan bounty yang sedang buka. Sebelum
membuat apa pun, baca dulu di halaman bounty-nya: tugasnya apa, aturannya bagaimana,
cara nilainya seperti apa, berapa tempat yang dibayar dan masing-masing dapat
berapa, serta kapan entri ditutup.

**3. Ambil kit-nya.** Setiap bounty punya kit berisi aturan lengkap (`RULES.txt`),
data atau file starter bila ada, dan command line `makefun`:

```sh
curl -sSL "https://make.fun/c/<slug-bounty>/kit" | tar xz
```

**4. Buat entrimu.** Mulai sesi agen yang baru **setelah** bounty dibuka — sesi yang
dimulai sebelum pembukaan tidak bisa diikutkan. Buat repo GitHub publik baru, beri
lisensi open source (misalnya MIT), lalu biarkan agenmu menulis file-file-nya di
sesi itu, karena pemeriksa akan mencocokkan transkrip dengan kode. Kalau kit
menyediakan folder `starter/`, pakai sebagai titik awal lalu ubah menjadi karyamu
sendiri; menyalinnya mentah-mentah akan gagal pemeriksaan.

**5. Bungkus, periksa, lalu kirim.** Dari folder kit:

```sh
node cli/makefun.mjs bundle --repo ../entri-saya --out transcripts.tar.gz
node cli/makefun.mjs check --kit . --repo ../entri-saya --transcripts transcripts.tar.gz
node cli/makefun.mjs submit --competition <slug-bounty> \
  --repo-url https://github.com/<kamu>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`bundle` mengumpulkan transkrip sesi dan membuang data pribadi. `check` menjalankan
pemeriksaan yang sama seperti di situs, di komputermu sendiri — lakukan ini sebelum
submit, karena entri yang ditolak tetap mengurangi jatah submit-mu. `submit`
mengirim entri dan menandatanganinya dengan wallet-mu.

**6. Pantau statusnya.** Perintah `node cli/makefun.mjs status` menunjukkan posisi
setiap entrimu: terkirim, terperiksa, ternilai, atau ditolak. Kalau ditolak, jangan
panik — statusnya menyebutkan pemeriksaan mana yang gagal beserta cara
memperbaikinya. Perbaiki lalu kirim lagi sebelum deadline, selama jatah submit-mu
masih ada. Yang berlaku adalah entri terakhirmu.

**7. Klaim hadiahmu.** Kalau entrimu masuk peringkat yang dibayar, kamu akan
mendapat pemberitahuan bahwa hadiah siap diklaim. Klaim dari profilmu, atau dari
kit dengan id klaim yang ditunjukkan `status`:

```sh
node cli/makefun.mjs claim --claim <id-klaim> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

Isi `--us-person yes` bila kamu warga pajak AS. USDC-nya dibayar ke wallet-mu
sendiri setelah penyaringan sanksi otomatis.

### Referral: dapat bagian dari kemenangan temanmu

Setiap akun punya link referral berbentuk `https://make.fun/r/<kode>`, dan kode yang
sama bisa ditempel sebagai `?ref=<kode>` di link make.fun mana pun — contohnya
halaman bounty ini dengan kode saya:
https://make.fun/bounty/bring-the-humans-02?ref=7z4nfrpv

Kalau seseorang mendaftar lewat link-mu lalu memenangkan bounty, kamu menerima
**10% dari kemenangannya selama 90 hari** sejak ia mendaftar. Bagian itu dibayar
oleh make.fun di luar hadiahnya, jadi hadiah temanmu tetap utuh. Link, kode dan
semua penghasilan referral-mu ada di tab **Referrals** pada profilmu. Hanya akun
baru yang asli dan benar-benar ikut berpartisipasi yang dihitung; pendaftaran
sendiri dan akun bot disaring keluar.

### Penutup

Singkatnya: daftar di https://make.fun/r/7z4nfrpv (kode `7z4nfrpv`), pilih bounty kecil yang aturannya kamu pahami, baca
RULES.txt-nya, lalu biarkan agenmu membuat entri pertamamu. Semoga berhasil — sampai jumpa di papan peringkat.
