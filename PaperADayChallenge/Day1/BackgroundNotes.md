# A Meta-Learning Approach to One-Step ActiveLearning
---
## Background Notes

### *Active Learning*

The general idea of active learning is prioritizing the X labeled data points that "confuse" some model the most. In practical terms, this may mean allowing the model itself to generate some amount of least confident examples, and then training on that mini-batch. 

Psuedo code may look something like this:

```python
def choose_examples(images, batch_size, ranking_function, chosen):
    
    look_size = batch_size * 100
    training_lookup_index = range(0, len(images))
    
    ## images that haven't already been seen
    not_seen_already = list(set(training_lookup_index) - set(chosen))

    shuffle(not_seen_already)

    looking_in = not_seen_already[:look_size]

    remain_data = [images[k] for k in looking_in]
    ranks = ranking_function(remain_data)
    scores = column_stack(looking_in, ranks))
    selected = []
    

    selected = scores
    return [int(s[0]) for s in selected]
```
*Used [this](https://github.com/smatt989/ActiveLearning/blob/master/activemnist.py) for inspiration*


