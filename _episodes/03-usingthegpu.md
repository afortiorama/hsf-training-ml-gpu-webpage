---
title: "Using the GPU"
teaching: 5
exercises: 15
questions:
- "How do I send my data to the GPU?"
- "How do I train my model on the GPU?"
objectives:
- "Examine the structure of a fully connected sequential neural network."
- "Look at the TensorFlow neural network Playground to visualize how a neural network works."
keypoints:
- "Neural networks consist of an input layer, hidden layers and an output layer."
- "TensorFlow Playground is a cool place to visualize neural networks!" 
---

# Sending the model to the GPU

~~~
model = Classifier_MLP(in_dim=input_size, hidden_dim=hidden_size, out_dim=num_classes).to(device=device)
~~~
{: .language-python}

# Sending the Data to the GPU

~~~
x_train, y_train = x_train.to(device), y_train.to(device)
~~~
{: .language-python}

> ## Challenge
> Adapt the training loop from the ML tutorial to use the GPU.
> 
> > ## Solution
> > 
> > ~~~
> > for batch, (x_train, y_train) in enumerate(train_loader):
> >         
> >         x_train, y_train = x_train.to(device), y_train.to(device)
> >         
> >         model.zero_grad()
> >         pred, prob = model(x_train)
> >         
> >         acc = (prob.argmax(dim=-1) == y_train).to(torch.float32).mean()
> >         train_accs.append(acc.mean().item())
> >         
> >         loss = F.cross_entropy(pred, y_train)
> >         train_loss.append(loss.item())
> >        
> >         loss.backward()
> >         optimizer.step()
> > ~~~
> > {: .language-python}
> {: .solution}
{: .challenge}