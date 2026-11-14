# Supercar Swipe

A Tinder-style static site for sorting 195 cars. Swipe left for **Not**, right for **Supercar**, or up (or the middle button) for **Hypercar**.

**Live site:** https://dmac817.github.io/Supercar-Swipe/

## How voting works

Each browser keeps a stable voter id from `crypto.randomUUID()`, stored in `localStorage`. A swipe sends that id and the car's slug (the image filename without `.jpg`) to the Supabase `cast_vote` function, which upserts the vote. Undo and Play again send a null vote, which deletes it.

The results screen reads `vote_counts`. Counts are also loaded when the page opens, so the list can paint from real totals. Vote requests are fire-and-forget: the deck never waits on the network, and a failed request stays silent.

Cars with no votes say so. Cars with fewer than five votes show the raw counts instead of a percentage, so one swipe is not presented as a consensus. Five or more votes show a split that adds up to 100%.

Your deck order, progress, and undo history stay in `localStorage` under `supercar-swipe-v3` and still work if a vote request fails. Photo credits are in the app.
