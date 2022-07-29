# Discord Self Service

The Self Service web portal for Discord

## Project Proposal

Many bots exist that enable users to assign themselves roles on a server, without having to pester those that have a higher privilege level to do it for them.

These bots generally take two forms, one form involves using reaction emoji to select options from a menu, and one form involves using the discord buttons API.

Both of these have clear shortcomings, both are difficult to keep perfectly in sync with the roles a server has as they change, reactions are messy and an unintuitive interface if you are not used to them, and buttons are not always perfectly clear. Often times the reaction will work as a toggle, so sometimes if the role has updated or been removed from you, you will need to unreact then re-react, which is also unintuitive. Roles are also lost if you leave or rejoin a server, and will need re-assignment.

Another common problem is needing new members to a server to fill out a form, which can be reviewed and approved by the server monerators. This often involves having a channel for submitting these in, with a pinned thread describing the information needed.

**All of this can be handled better using a self service portal.**

Discord Self Service aims to become this, providing a simple, easy way for users to configure their own roles, or apply to get access to a role.

The service is designed to have two component, a bot in the discord server which provides instructions and tutorials, and sends role application messages to be reviewed in by moderators discord, so that moderators do not need to check an external website. The second component is a website that users will be linked to in order to configure their self-assigned roles and submit applications.

## Workflow

The bot is added to a discord server, by the method usual for bots (discord oauth add a bot page).

The bot will create its own role and assign it to itself, and must be placed higher up the role list than any roles it is expected to manage automatically.

A person with administrator or manage server permissions sends the `/showtutorial` command to the bot in a channel. The bot will send a tutorial message in the channel, explaining how to use the bot to users. If a server does not wish to have this message permenantly somewhere, they may use `/help` to get the same message as an ephemeral secret message.

A person with the administrator or manage server permissions may send the `/configure` command to the bot, and will be sent an ephemeral secret message containing the URL they must access to configure the bot. This URL contains signed and encrypted information about the user creating the link, the and the roles they are allowed to set up, and how long the link is valid for (1 hour by default). A user is allowed to set up the roles that are lower in the list than the highest role they have that gives manage server permissions, or any role if they are an administrator.

Any user may send the `/selfservice` command, as instructed to by the message created by `/showtutorial` or `/help`. This will give them a URL in an ephemeral secret message that contains a signed and encrypted information as to which user created the link, and how long the self service link is valid for (4 hours) by default. From this page they will be able to assign themselves roles, and submit applications to be granted a role that requires an application.
