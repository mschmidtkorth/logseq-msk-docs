title:: config.edn

- The `logseq/config.edn` file located in your [[graph]] directory contains all of Logseq's user-changeable configuration.
- TODO Further examples
-
  #+BEGIN_TIP
  **Logseq updates** 
  Updates for Logseq may introduce new configuration options or change existing ones. Your `config.edn` is not migrated to a newer version when Logseq is updated to avoid losing your preferences. You have to do this manually by backing up your current `config.edn`, copying over the [latest online version](https://raw.githubusercontent.com/logseq/logseq/master/templates/config.edn) (or locally from the `/templates/` folder) and bringing back your configuration from your backup.
  #+END_TIP
## User Interface
	- ` :ui/show-empty-bullets?` (boolean) controls whether [[bullets]] should be shown in front of empty blocks
	- `:name/favorites "Homepage"` to change the name of the Favorites page
- ## Queries
	- {{embed ((610afd9a-36b6-475b-bdaa-e03c64ca3c0c)) }}