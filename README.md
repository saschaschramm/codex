# Codex

The purpose of this project is to evaluate the latest version of the Open AI language model `Codex`.

The table below presents the pass rates of the model on the [HumanEval](https://www.github.com/openai/human-eval) dataset.

| Model name | Pass@1 | Comment
| - | - | - |
| codex-12B | 28.81 | Best model published in [Evaluating Large Language Models Trained on Code](https://www.github.com/openai/human-eval)
| code-davinci-001 | 34.76 | https://openai.com/api/
| code-davinci-002 | 47.56 | https://openai.com/api/

## Magic strings 🪄
The performance of the `Codex` model can be increased by adding an additional string to a prompt. I call these strings `magic strings`.

| Magic string | Pass@1 |
| - | - |
| `Each step is commented.` | 54.88 |

### Completion with magic string
``` Python
def intersperse(numbers: List[int], delimeter: int) -> List[int]:
    """ Insert a number 'delimeter' between every two consecutive elements of input list `numbers'
    >>> intersperse([], 4)
    []
    >>> intersperse([1, 2, 3], 4)
    [1, 4, 2, 4, 3]
    
    Each step is commented.
    """
    # If the list is empty, return an empty list
    if not numbers:
        return []
    # If the list has only one element, return the list
    if len(numbers) == 1:
        return numbers
    # If the list has more than one element, return the first element,
    # followed by the delimeter, followed by the result of intersperse
    # on the rest of the list
    return [numbers[0], delimeter] + intersperse(numbers[1:], delimeter)
```
### Completion without magic string
``` Python
def intersperse(numbers: List[int], delimeter: int) -> List[int]:
    """ Insert a number 'delimeter' between every two consecutive elements of input list `numbers'
    >>> intersperse([], 4)
    []
    >>> intersperse([1, 2, 3], 4)
    [1, 4, 2, 4, 3]
    """
    result = []
    for i in range(len(numbers) - 1):
        result.append(numbers[i])
        result.append(delimeter)
    result.append(numbers[-1])
    return result
```

## Notes
Despite setting the temparature of the model to 0 the Open AI API is not completely determinisitic, so the performance of the model may vary over time.

## References 
The idea is similar to the idea presented in the paper [Large Language Models are Zero-Shot Reasoners](https://arxiv.org/pdf/2205.11916.pdf).


