# script for inputting a random combination of letters and returning an
# actual word in the dictionary

library(lexicon)
library(dplyr)
library(stringr)


#lexicon::available_data()

# obtain dataset to work from
df_words <- lexicon::freq_first_names %>%
  # add column for character count
  mutate(word = tolower(Name),
         num_characters = nchar(word)) %>%
  select(word, num_characters)
  
 
# word to find
output_word <- "dorothy"

# starting word
input_word <- "thydoro"

# filer dataset to match number of characters
input_characters <- nchar(input_word)

# filter dataset to same number of characters
df_words<- df_words %>%
  filter(num_characters == input_characters)



# turn input string to vector
input_vector <- as.vector(str_split_fixed(input_word, pattern = "",
                                          n = nchar(input_word)))


# create many random samples of input word
#sample(input_vector, size = nchar(input_word))

num_samples = 10000

df_search <- data.frame(rand_word = NA)
# when input_chracters == 9 & num_samples > 100,000 this loop is very slow
# however at input_charcter == 9 % num_samples 10,000 word is not found
# w
for(i in 1:num_samples){
  df_search[i, 'rand_word'] <- paste(sample(input_vector, size = nchar(input_word), replace = FALSE),
                                     sep = "",
                                     collapse = ""
  )
}

# Filter random words to match on in dictionary
df_search_reduced <- df_search %>%
  filter(rand_word %in% df_words$word)

# test if word was found
if (output_word %in% df_search_reduced$rand_word) {
  print("Your desired word was found!!!")
} else {
  print("No words found")
}

# all unique words
paste(unique(df_search_reduced$rand_word))

#### Appears to be working, but next step try word dictionary instead of names
#### names too unique to have high likelihood of returning multiple results


