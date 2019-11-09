# Hypha Co-op Chatbot: Roobot

> **Note:** For now, we're pretending the name of the chatbot is
> `roobot`, but that is up for debate. Consider it a placeholder.

Roobot is a friendly helper robot that lives in Hypha's chat rooms. It
helps us carry out routine tasks that we teach it to perform.

## Commands

The following commands can be run in chat via messages that address the
chatbot.

### `archive`

This command is used for archiving HackMD documentings in GitHub repos.

```
henry: hey all, how do we archive our public meetings now?
maria: @roobot archive https://hackmd.io/ERa1OsfKRranY-2sM1BcNQ
roboot: Yay! Archiving in progress!
        Waiting for public review at https://github.com/hyphacoop/organizing/pull/123
```

**Notice:** The below features of the `archive` command are
_not yet implemented_.

It can even be used to archiving private meetings, with `private:
true` in the YAML front-matter.

```
henry: what about when we have a private meeting like that last one?
maria: @roobot archive https://hackmd.io/uogV1UljQT633Vi6FfLK6g
roboot: Great! Archiving in progress!
roobot: Awaiting private review at https://gitlab.com/patcon/archive-demo-private/merge_requests/1
```

But what about when your meeting has public and private content? No
problem! You can just add a :lock: `:lock:` icon to each line in
question, and any content with a strikethrough on that line will be
censored from the public copy, and a full private backup will be created as
well.

```
henry: what about this meeting with sensitive parts?
maria: @roobot archive https://hackmd.io/RN8nBcqtS_CdcLycfD6cXQ
roboot: Great! Archiving in progress!
roobot: Awaiting public review at https://github.com/patcon/archive-demo/pull/2
roobot: Awaiting private review at https://gitlab.com/patcon/archive-demo-private/merge_requests/2
```

## Local Development

These instructions assume usage of the Heroku CLI.

1. **Configure** your local chatbot.
  - Create a `.env` file, using `sample.env` as guide. (Using `heroku
    config` might help to gather settings from hosted app.)
1. First, experiment with chatbot locally via its **terminal/shell adapter**.
  - Run `heroku local:run bin/hubot`
  - Experiment on command-line shell. (Note that this can still call out
    to production services if those access tokens are configured in `.env`.
1. Once satisfied, try running app with true **Matrix chat adapter**.
  - Spin down the live app: `heroku ps:scale web=0`
  - Run the app locally with Matrix chat adapter: `heroku local`
  - Experiment in Matrix/Riot chat room. E.g., `#hyphacoop-bot-testing:tomesh.net`
  - When done, spin up live app again: `heroku ps:scale web=1`
1. When you are satisfied, create a pull request against `master`
   branch.
  - Merging this pull request will deploy the changes live.

## Deployment

- We currently run our chatbot on Heroku.
- New code is auto-deployed from `master` branch via Heroku deployment.
- We manage uptime of chatbot via `hubot-heroku-keepalive`, which
  required [some important initial setup
tasks](https://github.com/hubot-scripts/hubot-heroku-keepalive#waking-hubot-up).
