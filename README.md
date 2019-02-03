# react-rails-ujs

[![npm version](https://badge.fury.io/js/react-rails-ujs.svg)](http://badge.fury.io/js/react-rails-ujs)
[![Downloads](http://img.shields.io/npm/dm/react-rails-ujs.svg)](https://npmjs.org/package/react-rails-ujs)

This npm package is replacement for [react-rails](https://github.com/reactjs/react-rails)
when assets pipeline is completely disabled and replaced with webpack bundles.

Created by [React Developers @ Selleo](https://selleo.com/react-expert-developers-team)

## Install

    npm i --save react-rails-ujs

Add react_component helper

    module ApplicationHelper
      def react_component(name, props = {}, options = {}, &block)
        html_options = options.reverse_merge(data: {
          react_class: name,
          react_props: (props.is_a?(String) ? props : props.to_json)
        })
        content_tag(:div, '', html_options, &block)
      end
    end

## Usage

Render components into rails views

    <%= react_component('Message', text: 'Hello react-rails-ujs') %>

Mount webpack bundled components

    import { mountComponents } from 'react-rails-ujs';
    
    import { Message } from './components/Message';
    
    mountComponents({
      Message,
    });

## Usage with React Hot Reload

    import React from 'react';
    import { AppContainer } from 'react-hot-loader';
    import { mountComponents } from 'react-rails-ujs';

    import { Message } from './components/Message';

    const render = (Component, props) => (
      <AppContainer><Component {...props}/></AppContainer>
    );

    mountComponents({
      Message,
    }, module.hot ? { render } : {});

## Usage with Redux

    import React from 'react';
    import { Provider } from 'react-redux'
    import { mountComponents } from 'react-rails-ujs';

    import createStore from './store/createStore';
    import { Message } from './components/Message';

    const store = createStore();

    const render = (Component, props) => (
      <Provider store={store}><Component {...props}/></Provider>
    );

    mountComponents({
      Message,
    }, { render });
