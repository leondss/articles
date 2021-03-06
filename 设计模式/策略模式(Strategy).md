---
title: 策略模式(Strategy)
date: 2016-11-2 20:36:50
categories: 设计模式
tags: 设计模式
---
定义算法族，分别封装起来，让它们之间可以互相替换，此模式让算法的变化独立于使用算法的客户。
<!-- more -->
# 示例

	public interface PackStrategy {
    	void execute();
	}

	public class BoxStrategy implements PackStrategy {
        @Override
        public void execute() {
            System.out.println("使用盒子包装");
        }
    }

    public class BagStrategy implements PackStrategy {
        @Override
        public void execute() {
            System.out.println("使用袋子包装");
        }
    }

    public class Fruit {
        private PackStrategy packStrategy;

        public Fruit(PackStrategy packStrategy) {
            this.packStrategy = packStrategy;
        }

        public void setPackStrategy(PackStrategy packStrategy) {
            this.packStrategy = packStrategy;
        }

        public void pack() {
            packStrategy.execute();
        }
    }

	public class App {
        public static void main(String[] args) {
            // 使用盒子包装
            Fruit fruit = new Fruit(new BoxStrategy());
            fruit.pack();

            // 使用袋子包装
            fruit.setPackStrategy(new BagStrategy());
            fruit.pack();
        }
    }
**PackStrategy**定义了包装的算法，**BoxStrategy，BagStrategy**分别实现使用盒子包装和袋子包装。**Fruit**声明**PackStrategy**变量，并配置动态改变其算法，完全由客户所决定。


# 使用场景
* 许多相关的类，他们的行为不同，通过策略模式提供了一种方法来配置一个类或者一个多个行为
* 封装多个算法，对客户端隐藏其实现