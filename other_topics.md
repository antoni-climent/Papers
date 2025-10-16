# ✨ Other topics

### Effective Skill Unlearning through Intervention and Abstention
**Paper:** https://arxiv.org/abs/2503.21730
**Summary:** It presents Neuron Adjustment and Key Space Detection. 
For NA it uses a Dataset with the skill to forget (ForgetD) and another with skills to keep (KeepD). It computes mean and standard deviation of each neuron preactivation and while in inference, if p(ForgetD) < p(KeepD), then modifies the preactivation so that it moves to the distribution that the KeepD creates in the neuron.
KSD  computes the mean and std after each activation layer for the ForgetD, getting an hipercube. If during inference the point goes inside the hipercube, it discarts the models answer.

Metrics show that it keeps better the knowledge that is out from the ForgetD.

Useful to learn how learning clusters in key spaces, but not ready for real applications. 
