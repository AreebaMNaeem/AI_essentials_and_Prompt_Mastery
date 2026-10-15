# Week 6: Introduction to AI Image Generation

> We start with how image generators work (GANs, then diffusion), then learn the three main tools, then generate our first images.

---

# This Week at a Glance

- How text-to-image models work (diffusion explained simply)
- Introduction to MidJourney: interface and basic prompting
- Introduction to DALL-E and Stable Diffusion
- Hands-on: generate a first set of images from text prompts

---

# Part 1: Before Diffusion, GANs

A **generative model** learns what a kind of data looks like (faces, landscapes, paintings) and then creates new examples of it.

## 1️⃣ How a GAN works

A GAN (Generative Adversarial Network) is **two models competing**:

- **Generator:** turns random noise into an image
- **Discriminator:** looks at an image and says "real" or "fake"

**Analogy:** a cook and a food judge.

- The **cook** tries to recreate a famous biryani (the generator)
- The **judge** has eaten the real biryani many times and says "real" or "copy" (the discriminator)
- Every time the judge says "copy", the cook adjusts the recipe
- The judge also gets sharper at spotting small differences
- After many rounds, the copy is so good that the judge can't tell it from the real one

```
Random noise
     │
     ▼
┌───────────┐
│ GENERATOR │
└─────┬─────┘
      │ fake image
      ▼
┌───────────────┐
│ DISCRIMINATOR │ ◀── real images (training data)
└───────┬───────┘
        │
        ▼
  "Real or Fake?"
        │
        ├──▶ generator learns what gave the fake away
        └──▶ discriminator learns to spot fakes better
```

**Training, repeated millions of times:**

1. The generator makes a fake image from noise.
2. The discriminator sees real and fake images and guesses which is which.
3. If it catches a fake, the generator learns what gave it away.
4. If it is fooled, the discriminator learns to look harder.

After training, the discriminator is thrown away. The generator makes an image from noise in **one quick step**.

## 2️⃣ Where GANs struggled

- **Fragile training:** the two models must stay balanced. If the discriminator gets too good, the generator gets no useful hint. If it is too weak, the generator never improves.
- **Mode collapse:** the generator settles on a few images that fool the discriminator, so there is little variety.
- **Moving target:** the generator is trying to fool a discriminator that keeps changing.
- **No clear progress score:** the training numbers don't show whether the images are getting better.
- **Narrow skills:** great at one kind of image, like faces, but weak at "anything you can describe."
- **Poor text control:** hard to tell a GAN what to draw in plain language.

Diffusion models were built to get around these problems. Let's see how they work.

---

# Part 2: Diffusion Models

## 1️⃣ What is a diffusion model?

Diffusion models are a class of deep neural networks that create images by **removing noise, step by step**.

The basic version, which learns from images alone, is called **unconditional diffusion**. Adding text to the training turns it into **conditional diffusion**, which is what text-to-image tools use. We will cover both.

## 2️⃣ Unconditional diffusion

Unconditional diffusion works in two phases:

- **Phase 1, forward diffusion:** noise is gradually added to a real image until it becomes pure static. Used **only in training**
- **Phase 2, reverse diffusion:** the model removes the noise step by step and recovers a clear image. The model learns this in training, and it is also how an image is **generated**

```
Forward diffusion (adds noise):     clear image  →  a bit noisy  →  very noisy  →  pure noise
Reverse diffusion (removes noise):  pure noise   →  rough shapes →  details     →  clear image
```

Adding the noise follows a fixed formula, so the model only has to learn the reverse. Once trained, it can start from pure static and create a brand-new image. Nothing tells the model what to create.

**Picture it like this:** a clear photo is slowly covered in TV static until nothing is visible. The model learns to clean the static off, one small step at a time.

### Training data

- Images only, with no captions

### Training steps

This happens once, before anyone types a prompt.

1. **Take a real image** from the dataset
2. **Add noise to it** (a little, a medium amount, or a lot, picked at random). This is **forward diffusion**
3. **Show the model** the noisy image and the step number, and ask: *"What noise was added?"*
4. **Compare** its answer with the real noise, which we know because we added it ourselves
5. **Adjust the model**, and repeat millions of times

Steps 3 to 5 are how the model learns **reverse diffusion**. Because we know the real answer every time, training is stable.

### What you get

- It starts from pure static and creates a random image that looks like its training data
- You have no control over what appears. A model trained on faces creates a random face

## 3️⃣ Conditional diffusion

To create images from **text**, the model needs something more. With it, the same process **transforms into conditional diffusion**.

### Training data

- Images **paired with captions**, like a photo of a cat with the caption "a cat"

### Training steps

The steps are the same as before, with the caption added:

1. **Take a real image and its caption**
2. **Add noise to the image** (forward diffusion), as before
3. **Show the model** the noisy image, the step number, **and the caption**, and ask: *"What noise was added?"*
4. **Compare** with the real noise, **adjust the model**, and repeat millions of times, as before

### What changes

- The model learns to remove noise **in a way that matches the caption**. A noisy image with the caption "a cat" should lose its noise in a cat-like way
- The caption is called the **condition**. A condition can also be a class label (like "dog") or another image
- **Generating:** you give your own condition (a prompt), and it guides every step
- **Text-to-image models are conditional diffusion models**

### Side by side

| | Unconditional diffusion | Conditional diffusion |
|---|---|---|
| **Training data** | Images only | Images paired with captions (or other conditions) |
| **What you give it when generating** | Nothing, just noise | Noise plus a condition, like a text prompt |
| **What you get** | A random image that looks like the training data | An image that matches your condition |
| **Your control** | None | You decide what appears |
| **Example** | A model trained on faces creates a random face | "a red cat in a spacesuit" creates that cat |

## 4️⃣ What happens when you press Generate

Example prompt: **"a red cat in a spacesuit"**

When you type a prompt, here is the big picture:

- The process starts with a canvas of **pure random noise**
- The model **removes noise gradually**, guided by your text
- At each step, the picture becomes less random and more like your description, until a clear image appears
- Because the starting noise is random, the same prompt can give different images each time

Behind the scenes, two things happen: your words are turned into numbers the model can use, and a picture of random static is turned into a clear image, guided by those numbers.

```
"a red cat in a spacesuit"
         │
         ▼
   Text encoder  ──▶  Embeddings (numbers that carry the meaning)
                           │
                           │  guide every step
                           ▼
Random noise ──▶  ┌─────────────────────┐
(static)          │       Denoiser      │ ──▶ Clean result ──▶ Decoder ──▶ Image
                  │  repeated 20-50×    │
                  └─────────────────────┘
```

### 1️⃣ Split the prompt into tokens

- The text is cut into small pieces called tokens
- Example: "a", "red", "cat", "in", "a", "space", "suit"

### 2️⃣ Turn the tokens into numbers

- A text encoder (CLIP, or T5 in some models) converts the tokens into **embeddings**: lists of numbers that capture the meaning of your prompt
- Similar words get similar numbers, so "cat" ends up close to "kitten"
- The image model uses these numbers as a **compass** during noise removal. This is why words about style, lighting, and composition change the result

### 3️⃣ Start with random noise

- The model creates an image made entirely of random static: the blank canvas
- Its size and shape come from the **resolution and aspect ratio** you choose, such as square for Instagram or wide for banners
- The **seed** sets this starting noise. A new seed gives a new image, and in tools that allow it, the same seed and prompt can reproduce similar results
- Stable Diffusion does this in a compressed space called **latent space**, which is much faster

### 4️⃣ Predict the noise

- The denoiser (a U-Net in many models, a transformer in newer ones) receives the noisy image, the step number, and your prompt's embeddings
- Its question is: **"Which part of this image is noise?"**
- Through **cross-attention**, each region of the image checks the prompt words that matter to it. The region becoming the cat's head looks at "cat" and "red", and the region around it looks at "spacesuit"

### 5️⃣ Guidance

- The model predicts the noise **twice**: once with your prompt and once without it
- The difference shows what your prompt adds, and the model pushes the result further in that direction:

```
final prediction = no-prompt prediction + guidance scale × (with-prompt − no-prompt)
```

- The **guidance scale** decides how hard to push. Higher follows your words more strictly, lower gives the model more freedom, and very high values can look harsh
- With a **negative prompt** (in some tools, a list of things you do not want), the model pushes away from it instead of from the empty prompt
- Good values differ between models, so don't copy settings from one model to another

### 6️⃣ Remove a little noise

- The **scheduler** removes only a portion of the predicted noise, not all of it
- Small steps let the model fix its own mistakes, while one big guess would look blurry

### 7️⃣ Repeat steps 4 to 6

- The loop runs 20 to 50 times. In some tools this is the **steps** setting
- Each round, the picture becomes less random and more like your description, until a clear image appears

### 8️⃣ Decode

- A decoder turns the clean, compressed result into the full-size image
- **Upscaling** can then increase its resolution, often with added detail

## 5️⃣ What the image looks like during the loop

Roughly, for our example:

| Stage | What you would see |
|---|---|
| **Start** | Pure static |
| **Early steps** | Blurry patches of color: a dark background and a red shape near the center |
| **Middle steps** | Clear shapes: the cat's body, the helmet, the moon |
| **Late steps** | Fine details: fur, reflections on the helmet, texture |
| **Decode** | The final full-size image |

The exact look depends on the model, but early steps always decide the layout and colors, and late steps add detail.

## 6️⃣ Useful related terms

| Term | What it means |
|---|---|
| **Prompt** | The text that guides the image |
| **Seed** | The number that sets the starting noise. In tools that allow it, the same seed and prompt can reproduce similar results |
| **Negative prompt** | In some tools, a list of things you do not want in the picture |
| **Steps** | How many denoising steps the model takes |
| **Guidance scale** | How strongly the image follows the prompt |
| **Resolution and aspect ratio** | The size and shape of the image, such as square for Instagram or wide for banners |
| **Upscaling** | Increasing an image's resolution, often with added detail |

Steps and guidance are settings in some tools, not all.

These details come from open models like Stable Diffusion, whose design is public. MidJourney and DALL-E may differ inside, and their full details aren't public.

## 7️⃣ Do we use forward diffusion when generating?

**No.** Forward diffusion is only for training. When you generate an image, **only the reverse process runs.**

| | Training | Generating |
|---|---|---|
| **Starts from** | A real image | Pure random static |
| **Forward diffusion** | Used: adds noise to the real image | Not used |
| **Reverse diffusion** | The model learns it | The model runs it |

Here is why:

- It makes noisy images and gives us the **real noise**, which is the answer key the model learns from
- When generating, there is no real image to add noise to
- The forward process is a **fixed formula**. All the learning is in the reverse

**How can removing noise from pure static give a picture?**
- The model has learned what real images look like
- At each step, it asks: "If a clean image were hiding under this static, which part is the noise?"
- Your prompt guides the answer, so the static slowly turns into the image you described

**One exception: image-to-image.** The tool adds some noise to your image first, then runs the reverse process with your prompt. More on this in Part 4.

## 8️⃣ Power and limitations of diffusion

| Power | Limitations |
|---|---|
| High quality and wide variety | Slower than GANs, since it takes many steps |
| Stable training | Needs a lot of computing power |
| Natural text control | Struggles with hands, text inside images, counting objects, and exact positions |
| Flexible: editing, filling in parts of an image | Can reflect bias from its training data |

---

# Part 3: GANs vs Diffusion

Now that we know how both work, here is how they compare:

| | GANs | Diffusion models |
|---|---|---|
| **Idea** | Two models compete | One model removes noise step by step |
| **Speed** | Fast, one pass | Slower, many steps |
| **Training** | Unstable | Stable |
| **Variety** | Can get stuck on a few outputs | Wide variety |
| **Text control** | Hard | Natural |
| **Still used for** | Real-time effects, upscaling, face tools | Most text-to-image tools |

GANs didn't disappear. They are still used, but they were hard to scale to "describe anything and get an image."

---

# Part 4: Text-to-Image and Image-to-Image

## 1️⃣ Text-to-image

- **Input:** a text prompt
- **Starts from:** pure random noise
- **Use it for:** creating a brand-new image from an idea

## 2️⃣ Image-to-image

- **Input:** an image plus a text prompt
- **Starts from:** your image with some noise added, not pure noise
- **Use it for:** changing the style, improving a sketch, or making variations of an image you already have

A setting called **strength** (or denoising strength) controls how much noise is added:

| Strength | Result |
|---|---|
| **Low** | Stays close to your original image |
| **High** | Changes it a lot, following the prompt more |

## 3️⃣ Related editing types

- **Inpainting:** change only a selected part of an image, like replacing the background
- **Outpainting:** extend an image beyond its original borders
- **Variations:** new versions of an existing image
- **Upscaling:** make an image larger and sharper

```
Text-to-image:   pure noise ────────────────→ reverse process + prompt → image
Image-to-image:  your image + some noise ───→ reverse process + prompt → new image
```

---

# Part 5: The Tools

## 1️⃣ MidJourney

- **What it is:** a paid image generator known for artistic, polished results
- **Where to use it:** the web app at midjourney.com, or Discord
- **How it works:** you type a prompt, and it gives you a grid of four images. You can then vary, upscale, or edit them
- **Version:** MidJourney releases new versions often. Check which one is the default, and use `--v` to pick one

**Basic prompting:** write your description in plain words, then add parameters at the end.

```
a red cat in a spacesuit, floating near the moon, watercolor painting, soft light --ar 16:9
```

| Parameter | What it does | Example |
|---|---|---|
| `--ar` | Aspect ratio (shape of the image) | `--ar 16:9` |
| `--stylize` (`--s`) | How much artistic style MidJourney adds | `--s 250` |
| `--chaos` | How different the four images are from each other | `--chaos 30` |
| `--seed` | Helps repeat a result | `--seed 123` |
| `--no` | Leave something out | `--no text` |
| `--v` | Pick the model version | `--v 7` |

Check MidJourney's own site for current plans, prices, and which parameters each version supports.

## 2️⃣ DALL-E (OpenAI)

- **What it is:** OpenAI's image generator. DALL-E 1 came in 2021, DALL-E 2 in 2022, and DALL-E 3 in 2023
- **Today:** ChatGPT's image generation uses newer **GPT Image** models, which are the successors to DALL-E. Many people still call it "DALL-E"
- **Where to use it:** inside ChatGPT, so you describe the image in a normal conversation
- **How it works:** you chat with it. There are no parameters to type. You say what you want, then ask for changes in plain words, like "make the background night" or "make it more cartoonish"
- **Image-to-image:** you can upload an image and ask it to change the style or edit parts of it
- **Good for:** beginners, fast results, and editing step by step through conversation

Access and limits depend on your ChatGPT plan, so check the current options.

## 3️⃣ Stable Diffusion

- **What it is:** an open family of image models from Stability AI, released in 2022. Because the model weights are available, people can run it on their own computer (with a suitable graphics card), use it through websites and apps, and customize it with community add-ons
- **Models:** SD 1.5 and SDXL are older. SD 3.5 is a more recent family (Large, Medium, and Large Turbo)
- **Where to use it:**
  - Free online demos (limited and sometimes slow)
  - **ComfyUI**, a free tool you can run on your own computer
  - Hosted services and the Stability AI API
- **Advanced features:** negative prompts, inpainting (changing part of an image), img2img (starting from your own image), and custom styles trained by users
- **Settings you control:** prompt, negative prompt, steps, guidance scale, seed, and strength for image-to-image
- **Strengths:** flexibility, control, and low cost once set up
- **Weaknesses:** it is more technical, and quality depends on the version, settings, and interface you choose
- **Running it locally:** needs a computer with a decent graphics card, and the models are large files
- **License:** SD 3.5 uses the Stability AI Community License, so check its terms before using images commercially

## 4️⃣ Which tool for what

| Tool | Best for | Control |
|---|---|---|
| **MidJourney** | Polished, artistic images | Medium (parameters) |
| **DALL-E / ChatGPT** | Beginners and conversational editing | Low (you describe in words) |
| **Stable Diffusion** | Learning, experimenting, and full control | High (all settings) |

## 5️⃣ The same ideas in each tool

| Idea | Stable Diffusion | MidJourney | ChatGPT |
|---|---|---|---|
| Shape of the image | Set width and height | `--ar` | Say it in words ("wide image") |
| Leave something out | Negative prompt | `--no` | Say it in words |
| Repeat a result | Seed | `--seed` | Not directly controllable |
| Follow the prompt more or less | Guidance scale | `--stylize` (style strength) | Not directly controllable |
| Change an existing image | Image-to-image and strength | Image prompts and variations | Upload it and describe the change |

> Tools update their versions, features, and plans often. Check each one before class.

---

# Part 6: Anatomy of a First Image Prompt

A good first prompt is one sentence built from a few simple parts. You don't need every part every time, but each part controls something different.

```
a red cat in a spacesuit, floating near the moon, watercolor painting, soft light, close-up
```

| Part | What it controls | In our example |
|---|---|---|
| **Subject** | What the image is about | a red cat in a spacesuit |
| **Setting** | Where it happens | floating near the moon |
| **Style** | How it looks (art style or medium) | watercolor painting |
| **Light and mood** | The lighting and feeling | soft light |
| **Composition** | The camera view or framing | close-up |
| **Tool settings** | Shape, exclusions, and so on, added the tool's own way | `--ar 16:9` in MidJourney |

## 1️⃣ Weak prompt vs stronger prompt

| Weak prompt | Stronger prompt |
|---|---|
| a cat | a red cat in a spacesuit, floating near the moon, watercolor painting, soft light, close-up |

A short prompt leaves everything to chance, so the model fills the gaps randomly. Each extra part narrows the choices.

## 2️⃣ Build it in three steps

1. **Start with the subject only:** "a red cat in a spacesuit"
2. **Add setting and style:** "..., floating near the moon, watercolor painting"
3. **Add light and composition:** "..., soft light, close-up"

Generate after each step and see what each part changes.

## 3️⃣ Where each part goes in each tool

- **ChatGPT:** write it as a normal sentence, then ask for changes in plain words
- **MidJourney:** write the description first, then add parameters like `--ar` at the end
- **Stable Diffusion:** write the description in the prompt box, and use the separate negative prompt box for things to avoid

**Quick tips**
- Be specific about the subject, and name the style you want
- Change **one thing at a time** so you can see what each change does
- Don't expect perfect hands or text inside the image
- Keep your prompts, because you will want to reuse the good ones

---

# Hands-On: Generate Your First Images

**Our prompt:**
```
a red cat in a spacesuit, floating near the moon, watercolor painting, soft light
```

## 1️⃣ Generate the same prompt in different tools

1. **ChatGPT:** generate the prompt and save the image
2. **Stable Diffusion:** run the same prompt (an online demo or ComfyUI) and note the steps, guidance scale, and seed you used
3. **MidJourney:** run it if you have access. If not, skip it and use the other two

## 2️⃣ Change one thing at a time

Change **only one thing** each time, then generate again and compare:

| Change | How |
|---|---|
| **Style** | Replace "watercolor painting" with "oil painting," "pixel art," or "3D cartoon" |
| **Shape** | `--ar 16:9` in MidJourney, or a wide size in Stable Diffusion |
| **Seed** | Press regenerate, or set a new seed, to see how the noise changes the result |
| **Guidance scale** | In Stable Diffusion, try a low value and a high one |
| **Negative prompt** | Add "blurry, extra fingers" |

## 3️⃣ Try image-to-image

1. Upload your favorite image from Step 1
2. Ask for a new style
3. In Stable Diffusion, try a low strength and a high strength, and compare

## 4️⃣ Write your own prompt

1. Write a prompt for something you like, using the parts from Part 6
2. Generate it in at least two tools

## 5️⃣ Fill in your log

Use this table for every image you generate:

| Tool | Prompt | What I changed | What happened |
|---|---|---|---|
| | | | |