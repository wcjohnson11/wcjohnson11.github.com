# Creating D3 Donuts for Mode

We use [Mode](www.modeanalytics.com) pretty extensively at Segment, and I've actually been fanboying hard since way before I started working at Segment when I first saw Derek Steer speak at SF Data Week about the value in sharing analysis and visualization to create communities. In short, they're aimed to be the Github of data analysis and visualization. If you haven't checked them out, go ahead and do so.

One of the things that we like most about it is that we can connect our Redshift cluster too it and easily share ad-hoc queries. Say I'm curious about how our latest batch of integrations are doing, I'll write up a SQL query in Mode, save it and then share it with a colleague who can fork my query and make their own modifications before sharing back to me.

<p><img src="./sharing.gif" alt=""></p>
Because sharing is caring

Another common use case is someone will put together a cool query and will send it to me and ask me if I can write some D3 for it. In addition to making it easy to share queries and their resulting data sets, they make it easy to write your own custom D3 to display the data however you want.

Today I'm making D3 Donuts, mmmmm

The data from your charts is available in Mode as `dataset.content` and you can pass that into the .data() function like you would any data to drive your documents.

### Be The Data
The first step in making any data visualization is understanding what the data looks look, in this case, it's an object with keys that are integration categories and values that are comma-delimited strings of the integrations for each category.

So off the bat I already know I'm going to need to turn those comma delimited strings into arrays of strings, split at the commas before I do anything else.
```js
var data = dataset.content[0];
  for (var key in data) {
    if (data[key] === "") continue;
	data[key] = data[key].split(', ');
};
```
The above will give me arrays of strings for categories with integrations and empty strings for categories with no integrations. A perfect starting line for making some visualization goodies since I'll be able to check the `data[key]`'s length and easily see how many integrations a given category has.


<p><img src="./donutdon.gif" alt=""></p>