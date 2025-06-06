<%"---"%>
banner: https://wallpapercave.com/wp/wp10166538.jpg
date-created: <% tp.file.creation_date("YYYY-MM-DD") %>
time: <% tp.file.creation_date("YYYY-MM-DD[T]HH:mm") %>
publish: false
type: my/emotion-tracker
emotion-group: <% await tp.system.suggester(
  ["Happiness", "Love", "Surprise", "Anger", "Sadness", "Fear", "Disgust"],
  ["Happiness", "Love", "Surprise", "Anger", "Sadness", "Fear", "Disgust"],
  false, "Select an emotion group:"
) %>
moodMeterEnergy: <% await tp.system.suggester(
  [
    "Energy",
    "5",
    "4",
    "3",
    "2",
    "1",
    "-1",
    "-2",
    "-3",
    "-4",
    "-5"
  ],
  [
    "",
    "5",
    "4",
    "3",
    "2",
    "1",
    "-1",
    "-2",
    "-3",
    "-4",
    "-5"
  ],
  false, "Select a mood meter energy rating:"
) %>
moodMeterPleasure: <% await tp.system.suggester(
  [
    "Pleasant",
    "5",
    "4",
    "3",
    "2",
    "1",
    "-1",
    "-2",
    "-3",
    "-4",
    "-5"
  ],
  [
    "",
    "5",
    "4",
    "3",
    "2",
    "1",
    "-1",
    "-2",
    "-3",
    "-4",
    "-5"
  ],
  false, "Select a mood meter pleasure rating:"
) %>
emotion: <% await tp.system.suggester(
  [ " ", "Happiness", "Joyful", "Content", "Pleasure", "Satisfied", "Grateful", "Amused", "Delighted", "Cheerful", "Jovial", "Blissful", "Proud", "Triumphant", "Optimistic", "Eager", "Hopeful", "Enthusiastic", "Excited", "Euphoric", "Enchanted" ],
  [ "", "Happy", "Joyful", "Content", "Pleasure", "Satisfied", "Grateful", "Amused", "Delighted", "Cheerful", "Jovial", "Blissful", "Proud", "Triumphant", "Optimistic", "Eager", "Hopeful", "Enthusiastic", "Excited", "Euphoric", "Enchanted" ],
  false, "Mood meter descriptors : happiness"
) %><% await tp.system.suggester(
  [ " ", "Love", "Romantic", "Affectionate", "Passionate", "Attracted", "Sentimental", "Compassionate", "Satisfied", "Peaceful", "Relieved" ],
  [ "", "Loving", "Romantic", "Affectionate", "Passionate", "Attracted", "Sentimental", "Compassionate", "Satisfied", "Peaceful", "Relieved" ],
  false, "Mood meter descriptors : love"
) %><% await tp.system.suggester(
  [ " ", "Surprise", "Moved", "Touched", "Amazed", "Astonished", "Shocked", "Confused", "Perplexed", "Dismayed", "Disillusioned" ],
  [ "", "Surprised", "Moved", "Touched", "Amazed", "Astonished", "Shocked", "Confused", "Perplexed", "Dismayed", "Disillusioned" ],
  false, "Mood meter descriptors : surprise"
) %><% await tp.system.suggester(
  [ " ", "Anger", "Displeasure", "Disgusted", "Contempt", "Annoyed", "Irritated", "Frustrated", "Agitated", "Aggravated", "Injustice", "Hostile", "Hateful", "Envious", "Jealous", "Enraged" ],
  [ "", "Angry", "Displeasure", "Disgusted", "Contempt", "Annoyed", "Irritated", "Frustrated", "Agitated", "Aggravated", "Injustice", "Hostile", "Hateful", "Envious", "Jealous", "Enraged" ],
  false, "Mood meter descriptors : displeasure"
) %><% await tp.system.suggester(
  [ " ", "Sadness", "Sorrowful", "Disappointed", "Dismayed", "Depressed", "Hurt", "Agonizing", "Displeased", "Shameful", "Regretful", "Guilty", "Neglected", "Isolated", "Lonely", "Despaired", "Grieving", "Powerless" ],
  [ "", "Sad", "Sorrowful", "Disappointed", "Dismayed", "Depressed", "Hurt", "Agonizing", "Displeased", "Shameful", "Regretful", "Guilty", "Neglected", "Isolated", "Lonely", "Despaired", "Grieving", "Powerless" ],
  false, "Mood meter descriptors : sadness"
) %><% await tp.system.suggester(
  [ " ", "Fear", "Scared", "Helpless", "Frightened", "Panicking", "Hysterical", "Insecure", "Inferior", "Inadequate", "Nervous", "Anxious", "Worried", "dreadful", "mortified" ],
  [ "", "Fearful", "Scared", "Helpless", "Frightened", "Panicking", "Hysterical", "Insecure", "Inferior", "Inadequate", "Nervous", "Anxious", "Worried", "dreadful", "mortified" ],
  false, "Mood meter descriptors : fear and worry"
) %><% await tp.system.suggester(
  [ " ", "Disgust", "Aversion", "Revulsion", "Contempt", "Loathing", "Distaste", "Nausea", "Abhorrence", "Repugnance" ],
  [ "", "Disgust", "Aversion", "Revulsion", "Contempt", "Loathing", "Distaste", "Nausea", "Abhorrence", "Repugnance" ],
  false, "Mood meter descriptors : disgust"
) %>
<%*
/* Filter for files that have "type: person" in their frontmatter */
const allFiles = app.vault.getMarkdownFiles();

const personFiles = allFiles.filter(file => {
    // Exclude files in the "00 Meta" folder 
  if (file.path.startsWith("00 Meta")) return false;
  const cache = app.metadataCache.getFileCache(file);
  if (!cache?.frontmatter) return false;

  const fm = cache.frontmatter;
  const typeVal = fm.type; 

  if (Array.isArray(typeVal)) {
    return typeVal.includes("person");
  } else if (typeof typeVal === "string") {
    return typeVal === "person";
  }
  return false;
});

// Debug
console.log("personFiles => ", personFiles.map(f => f.path));

const selectedFilePath = await tp.system.suggester(
  personFiles.map(f => f.basename),
  personFiles.map(f => f.path),
  false,
  "Select a file with type = person:"
);

const selectedFile = app.vault.getAbstractFileByPath(selectedFilePath);

// We store just the basename to link as [[basename]]
const whoWithBasename = selectedFile ? selectedFile.basename : "Unknown Person";
-%>
who-with: "[[<% whoWithBasename %>]]"
location: 
activity: 
comments: 
<%"---"%>

```meta-bind-embed
[[Emotion tracker - meta bind embed]]
```