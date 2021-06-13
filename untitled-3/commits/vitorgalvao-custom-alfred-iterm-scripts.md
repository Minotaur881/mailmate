# vitorgalvao/custom-alfred-iterm-scripts

## Commits on Aug 13, 2015

1.  [custom\_iterm\_script\_iterm\_2.9.applescript: cosmetic consistency impro…](https://github.com/vitorgalvao/custom-alfred-iterm-scripts/commit/01c24497b2f773e1cbde5a83a91343c1b713b399)

   ```text
   …vements

   + Some places used camelCase while others used_underscores
   + Some used the single line tell…to when available while others didn’t
       + Exception still made for 'tell the first terminal' since they’d become inconsistent with this rule applied
   + Indentation regarding where 'run script' ends is now clearer.
   + Corrected indentation in general
   ```

2.  [custom\_iterm\_script\_iterm\_2.1.1.applescript: cosmetic consistency imp…](https://github.com/vitorgalvao/custom-alfred-iterm-scripts/commit/7a6276db0e9a1042da535ef0ac53a4b58dd771d7)

   ```text
   …rovements

   + Some places used camelCase while others used_underscores
   + Some used the single line tell…to when available while others didn’t
       + Exception still made for 'tell the first terminal' since they’d become inconsistent with this rule applied
   + Indentation regarding where 'run script' ends is now clearer.
   + Deleted inconsistent blank line after first 'on run'
   + Corrected indentation inside first 'on run'
   ```

## Commits on Aug 10, 2015

1.  [Fixed search for iTerm/iTerm2 running](https://github.com/vitorgalvao/custom-alfred-iterm-scripts/commit/dc5beb7976eebce29d924a250f9caa8a395f031d)

   ```text
   The previous version of the applescript was not correctly opening a new session for each new command as it should be.

   Fixed this by correctly searching for either iTerm OR iTerm2 is_running.

   Signed-off-by: Stuart Ryan 
   ```

