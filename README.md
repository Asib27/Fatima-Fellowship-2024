# Fatima-Scholarship-2024
**Write up**:
* Explain what finetuning strategy you used and why

I finetuned `deepseek-ai/deepseek-math-7b-base` on bengali math problems dataset. There is no available math problem datasets in bangla. So i used `hkust-nlp/dart-math-uniform` and translated it to bengali using `facebook/nllb-200-3.3B`. Translations generated in this way lacks in quality. So, I splitted the english sentences and fed them separately to the translator. You can find the translation notebook in (data_creation.ipynb)[data_creation.ipynb]

Then i finetuned `deepseek-ai/deepseek-math-7b-base` with the data generated in the previous step. For finetuing LoRA with 4 bit quantization is used to meet compute requirements. Model is trained for 1 epoch. 

* Share some samples from the base model and from the final finetuned model. How do they compare?

For the given prompt: 
```
Problem: $f: \\mathbb{R} \\to \\mathbb{R}$ এমন একটি ফাংশন হতে হবে যে \\[f(x) f(y) - f(xy) = x + y\\] সব বাস্তব সংখ্যার জন্য $x$ এবং $y.$ $n$ হতে হবে $f(2),$ এর সম্ভাব্য মানের সংখ্যা, এবং $s$ হতে হবে $f(2) এর সম্ভাব্য মানের যোগফল।$ Find $ntimes s.$
```

Base model output:
```
Problem: $f: \mathbb{R} \to \mathbb{R}$ এমন একটি ফাংশন হতে হবে যে \[f(x) f(y) - f(xy) = x + y\] সব বাস্তব সংখ্যার জন্য $x$ এবং $y.$ $n$ হতে হবে $f(2),$ এর সম্ভাব্য মানের সংখ্যা, এবং $s$ হতে হবে $f(2) এর সম্ভাব্য মানের যোগফল।$
```

Final model output:
```
Solution: আমরা একটি সহজ উত্তর পাই $f(x) = 0,$ এবং $f(x) = 1,$ উভয় ফাংশনই সমীকরণটি সন্তুষ্ট করে। সুতরাং $n = 2$। এখন আমরা দেখি যে $f(2) = 1.$ যদি $f(2) = 0,$ তাহলে আমরা পাই $0 = 2,$ যা অসম্ভব। সুতরাং $s = 1,$ এবং $ns = 2.$ উত্তর হলঃ $2.$ উত্তর হলঃ $2.$ উত্তর হলঃ $2.$ উত্তর হলঃ $2.$ উত্তর হলঃ $2.$ উত্তর হলঃ $2.$ উত্তর হলঃ $2.$ উত্তর হলঃ $2.$ উত্তর হলঃ $2.$ উত্তর হলঃ $2.$ উ
```

We can see without finetuning the model returns the prompt. But with finetuning model generates some response . Although the response is not correct, but model is trained only for 1 epoch. With increased epoch it will achieve better performance. 

**Link to the model on Hugging Face Hub:** [LINK HERE]