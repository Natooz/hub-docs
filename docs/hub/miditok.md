# Using MidiTok at Hugging Face

`miditok` is an open-source library providing tokenizers for symbolic music, and especially [MIDI](https://fr.wikipedia.org/wiki/Musical_Instrument_Digital_Interface) files. It allows to easily use Transformers and sequence-based models with the symbolic music modality, for any task such as generation, transcription or synthesis.

## Exploring MidiTok in the Hub

You can find models using `miditok` filtering by library [models page](https://huggingface.co/models?library=miditok) or [full-text search](https://huggingface.co/search/full-text?q=miditok).

## Install the library

You can install `miditok` from pip (recommended way), or directly from the [GitHub repository](https://github.com/Natooz/MidiTok) if you want the latest features:

```bash
pip install miditok
```

```bash
pip install git+https://github.com/Natooz/MidiTok/
```

## Using existing models and tokenizers

`miditok` implements the same methods commonly used in the Hugging Face ecosystem to push and download models and tokenizers from the hub.

```python
from miditok import REMI

tokenizer = REMI.from_pretrained("YourUserName/model-name", token="your_hf_token")

tokens = tokenizer(Path("to", "midi.mid"))
gen_tokens = your_model.generate(tokens.ids)
```

Note that:

* :py:func:`miditok.MIDITokenizer.save_pretrained` is equivalent to calling :py:func:`miditok.MIDITokenizer.save_params`;
* :py:func:`miditok.MIDITokenizer.from_pretrained` can be used to load tokenizers whether from the Hugging Face hub or from a file on your local filesystem;
* for :py:func:`miditok.MIDITokenizer.save_pretrained` and :py:func:`miditok.MIDITokenizer.push_to_hub`, you can ignore the ``config`` argument which is meant to be used with models (not applicable for tokenizers);
* you can give a ``filename`` keyword argument with the :py:func:`miditok.MIDITokenizer.save_pretrained` and :py:func:`miditok.MIDITokenizer.from_pretrained` methods to use a specific tokenizer configuration file name, otherwise the default one will be used (``tokenizer.json``).

## Sharing your tokenizers/models

After training your models, we encourage you to share them on the hub!
You will also need to share the tokenizer so that users can use it.

```python
tokenizer.push_to_hub("YourUserName/model-name", private=True, token=hf_token)

# Sharing the model: this step will have to be done depending on the model's library
model.push_to_hub("YourUserName/model-name", private=True, token=hf_token)
```

## Additional resources

* [GitHub repository](https://github.com/Natooz/MidiTok);
* [Documentation](https://miditok.readthedocs.io)
* [Models in the Hub](https://huggingface.co/models?library=miditok&sort=trending)
